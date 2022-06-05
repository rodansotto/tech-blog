---
title: "SSRS: Automating Report Deployment using RS.EXE"
date: "2014-06-24"
categories: 
  - "sql-server"
---

I was looking for a way to deploy reports on the production server without going through the Report Manager and deploying one report at a time.  Then I stumbled upon [RS.EXE](http://msdn.microsoft.com/en-us/library/ms162839(v=sql.105).aspx), a scripting hosting utility that uses VB.NET script.  With VB.NET script you can deploy all your reports.

But how do you deploy SSRS reports in VB.NET?  Instead of creating one from scratch I searched the Internet and found one from John Desch’s blog [Using the RS.EXE utility to deploy a Report Server Project and Shared Dataset](http://blogs.msdn.com/b/johndesch/archive/2012/12/17/using-the-rs-exe-utility-to-deploy-a-report-server-project-and-shared-dataset.aspx).  It was said to be one of the best automated script available but one of the problems with the script is it does not support 2008SP1 which I need it to.

Good thing I found another script based on John Desch’s script but with enhancements including support for 2008SP1.  I found the script from Nishar’s blog [SSRS Deployment–Complete Automation–2012 & 2008](http://www.sqlblogspot.com/2014/03/ssrs-deploymentcomplete-automation2012.html). 

I slightly modified the _Commonscript.rss_ file for my own purposes.

'Begin Script  
  
Dim definition As \[Byte\]() = Nothing  
  
Dim bytedefinition As \[Byte\]() = Nothing  
  
Dim warnings As Warning() = Nothing  
  
  
  
'Main Entry point of utility  
  
Public Sub Main()  
  
    Console.WriteLine()  
  
    Console.WriteLine("Initiating Deployment")  
  
    rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
    Try  
  
        'Create the shared data source  
  
        CreateFolders(DataSourceFolderName, "/", "", "Visible")  
  
        'Create the folder that will contain the shared data sets  
  
        'CreateFolders(DataSetFolderName, "/", "", "Visible")  
  
        'Create the folder that will contain the deployed reports  
  
        CreateFolders(ReportFolderName, "/", "", "Visible")  
  
    Catch goof As Exception  
  
        Console.WriteLine(goof.Message)  
  
    End Try  
  
    ReadFiles(ReportSourcePath, "\*.rds")  
  
    'ReadFiles(ReportSourcePath, "\*.rsd")  
  
    ReadFiles(ReportSourcePath, "\*.rdl")  
  
    'Publish the report  
  
    'PublishReport(ReportName)  
  
    'UpdateDataSources(ReportFolderName, DataSourcePath)  
  
End Sub  
  
  
  
'Utility for creation of folders  
  
Public Sub CreateFolders(ByVal folderName As String, ByVal parentPath As String, ByVal description As String, ByVal visible As String)  
  
    Console.WriteLine()  
  
    Console.WriteLine("Checking for Target Folders")  
  
    'CatalogItem properties  
  
    Dim descriptionProp As New \[Property\]  
  
    descriptionProp.Name = "Description"  
  
    descriptionProp.Value = description  
  
    Dim visibleProp As New \[Property\]  
  
    visibleProp.Name = "Visible"  
  
    visibleProp.value = visible  
  
    Dim props(1) As \[Property\]  
  
    props(0) = descriptionProp  
  
    props(1) = visibleProp  
  
    Try  
  
        rs.CreateFolder(folderName, parentPath, props)  
  
        Console.WriteLine("Folder {0} successfully created", foldername)  
  
    Catch goof As SoapException  
  
        If goof.Message.Indexof("AlreadyExists") > 0 Then  
  
            Console.WriteLine("Folder {0} already exists", foldername)  
  
        End If  
  
    End Try  
  
End Sub  
  
  
  
'Utility for reading files from the Report Sevices Project  
  
Public Sub ReadFiles(filepath As String, fileextension As String)  
  
    Console.WriteLine()  
  
    Console.WriteLine("Reading Files from Report Services Project")  
  
    Dim rptdirinfo As System.IO.DirectoryInfo  
  
    rptdirinfo = New System.IO.DirectoryInfo(filepath)  
  
    Dim filedoc As FileInfo()  
  
    filedoc = rptdirinfo.GetFiles(fileextension)  
  
    Try  
  
        For rptcount As Integer = 0 To filedoc.Length - 1  
  
            If Not filedoc(rptcount).Name.ToString.Trim.ToUpper.Contains("BACKUP") Then  
  
                Select Case fileextension  
  
                    Case "\*.rds"  
  
                        CreateDataSource(filedoc(rptcount).tostring.trim)  
  
                    Case "\*.rsd"  
  
                        CreateDataSet(filedoc(rptcount).tostring.trim)  
  
                    Case "\*.rdl"  
  
                        PublishReport(filedoc(rptcount).tostring.trim)  
  
                End Select  
  
            End If  
  
        Next  
  
    Catch goof As Exception  
  
        Console.WriteLine("In ReadFiles " + goof.message)  
  
    End Try  
  
End Sub  
  
  
  
'Utility for Creating Shared Data Sets contained in the project  
  
Public Sub CreateDataSet(ByVal filename As String)  
  
    Dim valstart As Integer  
  
    Dim valend As Integer  
  
    Dim DSDefinitionStr As String  
  
    Dim DataSourceName As String  
  
    Dim QueryString As String  
  
    Try  
  
        Dim stream As FileStream = File.OpenRead(ReportSourcePath + "\\" + filename)  
  
        definition = New \[Byte\](stream.Length - 1) {}  
  
        stream.Read(definition, 0, CInt(stream.Length))  
  
        stream.Close()  
  
        For i As Integer = 0 To definition.Length - 1  
  
            DSDefinitionStr = DSDefinitionStr + Convert.ToString(Convert.ToChar(Convert.ToInt16(definition(i).ToString)))  
  
        Next  
  
        valstart = DSDefinitionStr.ToString.Indexof("<DataSourceReference>")  
  
        If valstart > 0 Then  
  
            valstart = DSDefinitionStr.ToString.IndexOf("<DataSourceReference>") + 21  
  
            valend = DSDefinitionStr.ToString.IndexOf("</DataSourceReference>")  
  
            DataSourceName = DSDefinitionStr.ToString.Substring(valstart, valend - valstart)  
  
            Console.WriteLine(DataSourceName)  
  
        End If  
  
    Catch e As IOException  
  
        Console.WriteLine(e.Message)  
  
    End Try  
  
    filename = filename.tostring.replace(".rsd", "")  
  
    Console.WriteLine("Attempting to Deploy DataSet {0}", filename)  
  
    Try  
  
        Dim item As CatalogItem  
  
        item = rs.CreateCatalogItem("DataSet", filename, "/" + DataSetFolderName, True, definition, Nothing, warnings)  
  
        If Not (warnings Is Nothing) Then  
  
            Dim warning As Warning  
  
            For Each warning In warnings  
  
                If warning.message.tostring.tolower.contains("refers to the shared data source") Then  
  
                    Console.WriteLine("Connecting DataSet {0} to Data Source {1}", filename, DataSourceName)  
  
                    Dim referenceData() As ItemReferenceData = rs.GetItemReferences("/" + DataSetFolderName + "/" + filename, "DataSet")  
  
                    Dim references(0) As ItemReference  
  
                    Dim reference As New ItemReference()  
  
                    Dim datasourceURL = "/" + DataSourcePath + "/" + DataSourceName  
  
                    reference.name = referenceData(0).Name  
  
                    Console.WriteLine("Reference name = " + reference.name)  
  
                    reference.Reference = datasourceURL  
  
                    references(0) = reference  
  
                    rs.SetItemReferences("/" + DataSetFolderName + "/" + filename, references)  
  
                Else  
  
                    Console.WriteLine(warning.Message)  
  
                End If  
  
            Next warning  
  
        Else  
  
            Console.WriteLine("DataSet: {0} published successfully with no warnings", filename)  
  
        End If  
  
    Catch goof As SoapException  
  
        If goof.Message.Indexof("AlreadyExists") > 0 Then  
  
            Console.WriteLine("The DataSet {0} already exists", fileName.ToString)  
  
        Else  
  
            If goof.Message.IndexOf("published") = -1 Then  
  
                Console.Writeline(goof.Message)  
  
            End If  
  
        End If  
  
    End Try  
  
    'UpdateDataSetSources(filename,DataSetFolderName, DataSourceFolderName,DataSourceName)  
  
End Sub  
  
  
  
'Utility for creating Data Sources on the Server  
  
Public Sub CreateDataSource(filename As String)  
  
    'Define the data source definition.  
  
    Dim dsDefinition As New DataSourceDefinition()  
  
    Dim DataSourceName As String  
  
    Dim valstart As Integer  
  
    Dim valend As Integer  
  
    Dim ConnectionString As String  
  
    Dim Extension As String  
  
    Dim IntegratedSec As String  
  
    Dim DataSourceID As String  
  
    Dim PromptStr As String  
  
    PromptStr = ""  
  
    Dim DSDefinitionStr As String  
  
    DSDefinitionStr = ""  
  
    DataSourceName = filename.tostring.trim.substring(0, filename.tostring.trim.length - 4)  
  
    Console.WriteLine("Attempting to Deploy Data Source {0}", DataSourceName)  
  
    Try  
  
        Dim stream As FileStream = File.OpenRead(ReportSourcePath + "\\" + filename)  
  
        bytedefinition = New \[Byte\](stream.Length - 1) {}  
  
        stream.Read(bytedefinition, 0, CInt(stream.Length))  
  
        stream.Close()  
  
        For i As Integer = 0 To bytedefinition.Length - 1  
  
            DSDefinitionStr = DSDefinitionStr + Convert.ToString(Convert.ToChar(Convert.ToInt16(bytedefinition(i).ToString)))  
  
        Next  
  
    Catch goof As IOException  
  
        Console.WriteLine(goof.Message)  
  
    End Try  
  
    If DSDefinitionStr.ToString.Contains("<ConnectString>") And DSDefinitionStr.ToString.Contains("</ConnectString>") Then  
  
        valstart = DSDefinitionStr.ToString.IndexOf("<ConnectString>") + 15  
  
        valend = DSDefinitionStr.ToString.IndexOf("</ConnectString>")  
  
        ConnectionString = DSDefinitionStr.ToString.Substring(valstart, valend - valstart)  
  
    End If  
  
    If DSDefinitionStr.ToString.Contains("<Extension>") And DSDefinitionStr.ToString.Contains("</Extension>") Then  
  
        valstart = DSDefinitionStr.ToString.IndexOf("<Extension>") + 11  
  
        valend = DSDefinitionStr.ToString.IndexOf("</Extension>")  
  
        Extension = DSDefinitionStr.ToString.Substring(valstart, valend - valstart)  
  
    End If  
  
    If DSDefinitionStr.ToString.Contains("<IntegratedSecurity>") And DSDefinitionStr.ToString.Contains("</IntegratedSecurity>") Then  
  
        valstart = DSDefinitionStr.ToString.IndexOf("<IntegratedSecurity>") + 20  
  
        valend = DSDefinitionStr.ToString.IndexOf("</IntegratedSecurity>")  
  
        IntegratedSec = DSDefinitionStr.ToString.Substring(valstart, valend - valstart)  
  
    End If  
  
    If DSDefinitionStr.ToString.Contains("<DataSourceID>") And DSDefinitionStr.ToString.Contains("</DataSourceID>") Then  
  
        valstart = DSDefinitionStr.ToString.IndexOf("<DataSourceID>") + 14  
  
        valend = DSDefinitionStr.ToString.IndexOf("</DataSourceID>")  
  
        DataSourceID = DSDefinitionStr.ToString.Substring(valstart, valend - valstart)  
  
    End If  
  
    If DSDefinitionStr.ToString.Contains("<Prompt>") And DSDefinitionStr.ToString.Contains("</Prompt>") Then  
  
        valstart = DSDefinitionStr.ToString.IndexOf("<Prompt>") + 8  
  
        valend = DSDefinitionStr.ToString.IndexOf("</Prompt>")  
  
        PromptStr = DSDefinitionStr.ToString.Substring(valstart, valend - valstart)  
  
    End If  
  
    dsdefinition.CredentialRetrieval = CredentialRetrievalEnum.Integrated  
  
    dsdefinition.ConnectString = ConnectionString  
  
    dsdefinition.Enabled = True  
  
    dsdefinition.EnabledSpecified = True  
  
    dsdefinition.Extension = extension  
  
    dsdefinition.ImpersonateUser = False  
  
    dsdefinition.ImpersonateUserSpecified = True  
  
    'Use the default prompt string.  
  
    If PromptStr.ToString.Length = 0 Then  
  
        dsdefinition.Prompt = Nothing  
  
    Else  
  
        dsdefinition.Prompt = PromptStr  
  
    End If  
  
    dsdefinition.WindowsCredentials = False  
  
    Try  
  
        rs.CreateDataSource(DataSourceName, "/" + DataSourceFolderName, False, dsdefinition, Nothing)  
  
        Console.WriteLine("Data source {0} created successfully", DataSourceName.ToString)  
  
    Catch goof As SoapException  
  
        If goof.Message.Indexof("AlreadyExists") > 0 Then  
  
            Console.WriteLine("The Data Source name {0} already exists", DataSourceName.ToString)  
  
        End If  
  
    End Try  
  
End Sub  
  
  
  
'Utility to Publish the Reports  
  
Public Sub PublishReport(ByVal reportName As String)  
  
    Try  
  
        Dim stream As FileStream = File.OpenRead(ReportSourcePath + "\\" + reportName)  
  
        definition = New \[Byte\](stream.Length - 1) {}  
  
        stream.Read(definition, 0, CInt(stream.Length))  
  
        stream.Close()  
  
    Catch e As IOException  
  
        Console.WriteLine(e.Message)  
  
    End Try  
  
    reportname = reportname.tostring.replace(".rdl", "")  
  
    Console.WriteLine("Attempting to Deploy Report Name {0}", reportname.tostring)  
  
    Dim item As CatalogItem  
  
  
    Try  
  
        item = rs.CreateCatalogItem("Report", reportname, "/" + ReportFolderName, True, definition, Nothing, warnings)  
  
        'warnings = rs.CreateCatalogItem(reportName, "/" + ReportFolderName, False, definition, Nothing)  
  
        If Not (warnings Is Nothing) Then  
  
            If item.Name <> "" Then  
  
                Console.WriteLine("Report: {0} published successfully with warnings", reportName)  
                UpdateDataSources\_report(reportName)  
                UpdateDataSet\_report(reportName)  
            Else  
  
                Dim warning As Warning  
  
                For Each warning In warnings  
  
                    Console.WriteLine(warning.Message)  
  
                Next warning  
  
            End If  
  
        Else  
  
            Console.WriteLine("Report: {0} published successfully with no warnings", reportName)  
            UpdateDataSources\_report(reportName)  
            UpdateDataSet\_report(reportName)  
        End If  
  
    Catch goof As SoapException  
  
        If goof.Message.Indexof("AlreadyExists") > 0 Then  
  
            Console.WriteLine("The Report Name {0} already exists", reportName.ToString)  
  
        Else  
  
            If goof.Message.IndexOf("published") = -1 Then  
  
                Console.WriteLine(goof.Message)  
  
            End If  
  
        End If  
  
    End Try  
  
End Sub  
  
  
  
'Utility to Update The Data Sources on the Server  
  
Public Sub UpdateDataSources(ReportFolderName As String, DataSourcePath As String)  
  
    rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
    Dim item As CatalogItem  
  
    Dim items As CatalogItem()  
  
    Try  
  
  
  
        items = rs.ListChildren("/" + ReportFolderName, False)  
  
        For Each item In items  
  
            'Console.WriteLine("          update date source called     --------"+ item.Path + " -----------")  
  
            If item.path.Indexof("rdl") > 0 And ReportName = "" Then  
  
                'Console.WriteLine("          update date source called     --------"+ item.path.Indexof("rdl").tostring() + " -----------")  
  
                Dim dataSources() As DataSource = rs.GetItemDataSources(item.Path)  
  
                For Each ds As DataSource In dataSources  
  
                    Dim sharedDs(0) As DataSource  
  
                    sharedDs(0) = GetDataSource(DataSourcePath, ds.Name)  
  
                    rs.SetItemDataSources(item.Path, sharedDs)  
  
                    Console.WriteLine("Set " & ds.Name & " datasource for " & item.Path & " report")  
  
                    'end if  
                Next  
  
            End If  
  
        Next  
  
        If ReportName = "" Then  
  
            Console.WriteLine("Shared data source reference set for reports in the {0} folder.", ReportFolderName)  
  
        End If  
  
  
        If ReportName <> "" Then  
  
            '    Console.WriteLine("               " + "/" + ReportFolderName + "/" + ReportName + "  ------------- second  update called        ---------------------- ")  
  
            Dim dataSources() As DataSource = rs.GetItemDataSources("/" + ReportFolderName + "/" + ReportName)  
  
            For Each ds As DataSource In dataSources  
  
                Dim sharedDs(0) As DataSource  
  
                sharedDs(0) = GetDataSource(DataSourcePath, ds.Name)  
  
                rs.SetItemDataSources("/" + ReportFolderName + "/" + ReportName, sharedDs)  
  
                Console.WriteLine("Set " & ds.Name & " datasource for " & "/" + ReportFolderName + "/" + ReportName & " report")  
  
                'end if  
            Next  
  
            Console.WriteLine("All the shared data source reference set for report {0} ", "/" + ReportFolderName + "/" + ReportName)  
  
        End If  
  
    Catch goof As SoapException  
  
        Console.WriteLine(goof.Detail.InnerXml.ToString())  
  
    End Try  
  
End Sub  
  
  
  
  
'Utility to Update The Data Sources on the Server  
  
Public Sub UpdateDataSources\_report(ReportName As String)  
  
    rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
    Dim item As CatalogItem  
  
    Dim items As CatalogItem()  
  
    Try  
  
        'If ReportName <> "" then  
  
        '    Console.WriteLine("               " + "/" + ReportFolderName + "/" + ReportName + "  ------------- second  update called        ---------------------- ")  
  
        Dim dataSources() As DataSource = rs.GetItemDataSources("/" + ReportFolderName + "/" + ReportName)  
  
        For Each ds As DataSource In dataSources  
  
            Dim sharedDs(0) As DataSource  
  
            sharedDs(0) = GetDataSource(DataSourcePath, ds.Name)  
  
            rs.SetItemDataSources("/" + ReportFolderName + "/" + ReportName, sharedDs)  
  
            Console.WriteLine("Set " & ds.Name & " datasource for " & "/" + ReportFolderName + "/" + ReportName & " report")  
  
            'end if  
        Next  
  
        Console.WriteLine("All the shared data source reference set for report {0} ", "/" + ReportFolderName + "/" + ReportName)  
  
        'end if      
  
  
    Catch goof As SoapException  
  
        Console.WriteLine(goof.Detail.InnerXml.ToString())  
  
    End Try  
  
End Sub  
  
  
  
'Utility to link The Dataset with the Report  
  
Public Sub UpdateDataSet\_report(ReportName As String)  
  
    rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
  
    Try  
  
        Dim dataSets As ItemReferenceData() = rs.GetItemReferences("/" + ReportFolderName + "/" + ReportName, "DataSet")  
  
        If dataSets IsNot Nothing AndAlso dataSets.Length > 0 AndAlso Not String.IsNullOrEmpty(dataSets(0).Name) Then  
  
            For i As Integer = 0 To dataSets.Length - 1  
  
                Dim references(0) As ItemReference  
                Dim sharedDataSet = New ItemReference()  
                sharedDataSet.Name = dataSets(i).Name  
                Console.WriteLine("Attempting to Link Dataset {0}", dataSets(i).Name)  
                sharedDataSet.Reference = "/" + DataSetFolderName + "/" + dataSets(i).Name  
                references(0) = sharedDataSet  
                rs.SetItemReferences("/" + ReportFolderName + "/" + ReportName, references)  
                Console.WriteLine("Report " + ReportName + " Linked to data set " + "/" + DataSetFolderName + "/" + Convert.ToString(sharedDataSet.Name))  
            Next  
  
        End If  
  
    Catch goof As SoapException  
  
        Console.WriteLine(goof.Detail.InnerXml.ToString())  
  
    End Try  
  
End Sub  
  
  
  
  
'Function to Reference Data Sources  
  
Private Function GetDataSource(sharedDataSourcePath As String, dataSourceName As String) As DataSource  
  
    Dim reference As New DataSourceReference()  
  
    Dim ds As New DataSource  
  
    reference.Reference = "/" + sharedDataSourcePath & "/" & dataSourceName  
  
    ds.Item = CType(reference, DataSourceDefinitionOrReference)  
  
    ds.Name = dataSourceName  
  
    Console.WriteLine("Attempting to Link Data Source {0}", ds.Name)  
  
    GetDataSource = ds  
  
End Function  

  

I also modified the _deploy.bat_ file as well.

set ServerPath=http://localhost/ReportServer  
set DataSourceFolderName=Data Sources  
set DataSourcePath=Data Sources  
set DataSetFolderName=Datasets  
set ReportFolderName=My Reports  
set ReportSourcePath=.\\My Reports  
set ReportName=  
      
rs.exe   
\-i Commonscript.rss   
\-s %ServerPath%   
\-v DataSourceFolderName="%DataSourceFolderName%"   
\-v DataSourcePath="%DataSourcePath%"   
\-v DataSetFolderName="%DataSetFolderName%"   
\-v ReportFolderName="%ReportFolderName%"   
\-v ReportSourcePath="%ReportSourcePath%"   
\-v ReportName="%ReportName%"   
\-e Mgmt2010
