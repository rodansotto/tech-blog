---
title: "C#: Quick Review on Raising Events"
date: "2014-05-21"
categories: 
  - "c-sharp"
---

To illustrate raising events, let’s pick a very simple but classic example of a publisher and subscriber relationship.  Note that events make use of delegates and if you need to brush up on delegates, check my post [here](http://rodansotto.wordpress.com/2014/05/16/c-quick-review-on-delegates/ "C#: Quick Review on Delegates").

// So here you have a publisher class
public class Publisher
{
    // Inside you declare a public event
    // And the delegate type for the event is EventHandler
    public event EventHandler Published;
    
    // The event needs to be public to allow public subscription
    //  (e.g. p.Published += Subscriber1)
    // Also one might ask why we need the event keyword when, without it,
    //  making it a delegate, it basically does the same thing
    // Well, declaring an event lets you raise the event privately, but
    //  still allow public subscription
    // With a public delegate, anyone can remove other people's event
    //  handlers, raise the events themselves, etc. - an encapsulation
    //  disaster
    // Also when it's declared an event, it will appear in the list
    //  of properties with a lightning icon beside it
    
    // So EventHandler is a delegate type that accepts an object and an 
    //  EventArgs parameters and returns void
    // You can code the following instead and it will do the same thing
    public delegate void PublishedEventHandler(object sender, EventArgs e);
    public event PublishedEventHandler Published;
    
    // You can actually use a different event parameter if you prefer, 
    //  but that will mean not following the standard event handling
    public delegate void PublishedEventHandler(string title);
    public event PublishedEventHandler Published;
    
    // Also, using EventArgs for your event handler means you can't pass
    //  any event data to your event handler
    // If you need to pass data, you can use any event data type (like a
    //  string in the example above) or class.
    // Standard practice is to use an event data class derived from
    //  EventArgs and this will also require you to define a custom event
    //  handler delegate type
    public class PublishedEventArgs : EventArgs
    {
        public string Title { get; set; }
    }
    public delegate void PublishedEventHandler(object sender, 
                                                PublishedEventArgs e);
    public event PublishedEventHandler Published;
    
    
    // Next, you raise the event with the following method
    // The method needs to be protected and virtual so that any derived
    //  classes can override it if necessary
    protected virtual void OnPublished(EventHandler e)
    {
        EventHandler handler = Published;
        if (handler != null)
        {
            // Here we are calling the delegate which in turn invokes all
            //  the methods in it's invocation list (if there is more than
            //  one method to invoke)
            handler(this, e);
        }
    }    
    
    // Then the following public method just provides the publisher a
    //  means to notify it's subsribers of a newly published title
    public void Publish()
    {
        OnPublished(null);
    }

    // But if you are passing event data...
    protected virtual void OnPublished(PublishedEventArgs e)
    {
        PublishedEventHandler handler = Published;
        if (handler != null)
        {
            handler(this, e);
        }
    }
    
    public void Publish()
    {
        PublishedEventArgs e = new PublishedEventArgs();
        e.Title = "Hello World!!!";
        OnPublished(e);
    }    
}
    
    
// Somewhere in code outside the Publisher class, you have the following 
//  subscribers or event handlers
static void Subscriber1(object sender, EventArgs e)
{
    Console.WriteLine("Subscriber1 notified of new title");
}
    
static void Subscriber2(object sender, EventArgs e)
{
    Console.WriteLine("Subscriber2 notified of new title");
}
    
// Again, if you are passing event data...
static void Subscriber1(object sender, PublishedEventArgs e)
{
    Console.WriteLine("Subscriber1 notified of new title " + e.Title);
}
    
// Lastly, here you instantiate a publisher,
//  add the following subscribers,
//  and then publish a new title
Publisher p = new Publisher();
p.Published += Subscriber1;
p.Published += Subscriber2;
p.Publish();
