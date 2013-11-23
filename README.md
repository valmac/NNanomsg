## NNanomsg

This is a lightweight wrapper around the <a href="http://nanomsg.org">nanomsg</a> C API which makes
it callable from .NET languages.

NNanomsg can be used without recompiling on any platform where .NET is available. At runtime, it needs 
to be able to locate the native nanomsg library for your platform as well as nanomsgx, a small library
written in C which implements polling functionality that is provided as part of this distribution. We
have included nanomsg and nanomsgx binaries for Windows (x86/x64) and Linux (x86/x64).

The search path for these libraries is:

     Windows:   [Application Directory]\[x86|x64]
                [Application Directory]

     Posix:     [Application Directory]/[x86|x64]
                [Application Directory]
                /usr/local/lib
                /usr/lib

The advantages of wrapping the C API rather than implementing it entirely in a .NET language are:
 1. It is much less work. This means that:
 2. There is very little code in which to introduce bugs. 

The disadvantages are:
 1. .NET applications that use the library cannot be run on different platforms without acquiring/building nanomsg
    and nanomsgx for those platforms.
 2. It means you might have to bugger about with C compilers / native linking which depending on your luck and level 
    of expertise has the potential to cause headaches.
 3. I'm not sure which method is more efficient. 

### Example

A simple C# example is included in the source distribution and you might also want to look at the Test project.

These are a work in progress. 

### Usage

NNanomsg actually exposes API's at three levels of abstraction:

 1. Static methods in the NN class. These match those of the C API very closely.
 2. NanomsgSocket, which provides more convenience functionality than the NN methods.
 3. Protocol classes: PairSocket, PublishSocket, SubscribeSocket etc. which restrict the allowed operations to
    those apporpriate to the associated socket type.

For most applications, the protocol classes should be used.


### Development Status

Alpha quality. 

Tested against nanomsg version 0.2-alpha only.

We're still debating the best way to structure some functionality and parts of the API will change.

Polling functionality could probably be implemented completely in managed code (thus getting rid of the extra 
native library) and more properly integrated with the .NET runtime / ThreadPool. Some aspects of this task
are quite difficult however and the present implementation works well enough for me and I suspect most people.

I've been using this binding quite a bit in a fairly large project that was previously using 0mq. Everyhing
seems to be running smoothly.


### Building Notes

A Vagrantfile that builds a VM with nanomsg and mono installed which can be used to run the example project 
is included.


### Primary Contributors

  * Matt Howeltt
  * Mason Of Words
