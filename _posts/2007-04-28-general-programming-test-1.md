---
title: "General: Programming Test #1"
date: "2007-04-28"
categories: 
  - "general"
---

There was this test in one of the job interviews I had recently that I did not ace well.  It was a written programming test.  I have not been given a written programming test for a while so I was caught off-guard.  If this was a hands-on, I would have aced it.  Anyways, here is some more details about the problem.

Given an input of 1-7 indicating the day of the week (Sunday being a 1, Monday a 2, and so on...) for the first day of the month, print a calendar for that month.  I fired my Visual Studio 2005 and started coding in VB.  After 3 iterations of the code (I like to make my code small and easy to understand which is why I usually do more than 1 iterations of the code), I came up with this solution:

    Public Sub PrintMonthCalendar(ByVal DayOfWeekFirstDayOfMonth As Integer, _
                                    ByVal NumberOfDaysInMonth As Integer)
        Dim i As Integer
        Dim intDay As Integer = 1

        Console.WriteLine("Su Mo Tu We Th Fr Sa ")
        For i = 1 To NumberOfDaysInMonth + (DayOfWeekFirstDayOfMonth - 1)
            If i < DayOfWeekFirstDayOfMonth Then
                Console.Write("   ")
            Else
                If i Mod 7 = 0 Then
                    Console.WriteLine("{0,2} ", intDay)
                Else
                    Console.Write("{0,2} ", intDay)
                End If
                intDay += 1
            End If
        Next

        Console.ReadLine()
    End Sub

Here are some sample outputs of the program:

![]({{ site.baseurl }}/assets/images/clip_image0021.jpg)


