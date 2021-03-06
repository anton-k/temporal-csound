
The library joins the forces of the packages temporal-music-notation 
and csound-expression. The former package gives you handy primitives to arrange the events
in sequences (like parallel or sequential composition, the tempo change,
standard names for notes and durations) and the later is used for
creation of musical timbres or software synthesizers. 

You can find the short intro in the module "Csound".

* The tutorial for 
    [csound-epression package (timbres)](https://github.com/anton-k/csound-expression/blob/master/tutorial/QuickStart.markdown) 

* The tutorial for temporal-music-notation package (composition)
         and temporal-music-notation-western package (standard names for notes): see [module Csound](hackage.haskell.org/package/temporal-csound-0.3.0/docs/Csound.html)     
    

This library defines standard note representation that let's you 
invoke csound instruments with notes defined in the package temporal-music-notation.
    
Also this library provides you with some cool instruments to try the things out (see "Csound.Patch").
    
**WARNING**: the library works best within ghci. The real-time sound rendering function dac spawns
    a child process in the background which may continue to execute after you stop the main process that runs the programm.
    It's not so in vim but it happens in the Sublime Editor and when you invoke runhaskell. So the best
    is to write you program in the separate file and then load it in the ghci and invoke the function main (which
    runs the sound rendering with the function dac). 
    
Library strives to be very simple. For example, to trigger the instrument with virtual midi-device is
as simple as (in ghci with loaded modules "Csound" and "Csound.Patch")

~~~
> Csound Csound.Patch> vdac $ mul 0.2 $ largeHall $ onMidi stringPad
~~~   

If you have a connected hardware midi-device you can just type:
    
~~~
> Csound Csound.Patch> dac $ mul 0.2 $ largeHall $ onMidi stringPad
~~~
    
And you are ready to go. To play a C-major chord just do:

~~~
> Csound Csound.Patch> dac $ mul 0.2 $ magicCave $ mix $ notes vibraphone2 $ mel [c, e, g, high c, rest 15]
~~~
    
Here we send the output to speakers (`dac` or `vdac`), scale the signal to make it quiter (`mul`), 
place the signal in some room with reverberation (`largeHall` or `magicCave`), listen to midi
events (`onMidi` or `onMidin` for a midi on the given channel) or get the signal from scores (`mix`),
trigger the csound instrument (`stringPad` or `vibraphone2`) on events (`notes`) and construct
the events in sequence (`mel`). Events include notes (`c`, `e`, `g` - C major) and rests (`rest`).

