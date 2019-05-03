# Xamarin-binding-library-Socked.io-java-client


[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Instalacion
Compile el projecto y a#ada una referencia en su proyecto xamarin.android a socketandroid.dll
## Uso
Implementado oyente
```
    public class ListenerEventArgs : System.EventArgs
    {
        public Java.Lang.Object[] data { get; set; }
    }

    public class listener : Java.Lang.Object, IO.Socket.Emitter.Emitter.IListener
    {
        public delegate void CustomEventHandler(object Sender, ListenerEventArgs args);
        public event CustomEventHandler Listener;
        
        public void Call(params Java.Lang.Object[] p0)
        {
            if (Listener != null)
            {
                var args = new ListenerEventArgs
                {
                    data = p0
                };
            }
        }
    }
```
   
Escuchando evento
```
    var socket = IO.Socket.Client.IO.Socket("http://localhost");
    var MessageEvent = new listener();
    MessageEvent.Listener += (Sender, args) =>
    {
        Console.WriteLine(args.data);
    };
    socket.On(Socket.EventConnect, MessageEvent);
    socket.Connect();
```

Emitiendo eventos
```
    socket.Emit("mensaje", "hello from pakistan");
```
