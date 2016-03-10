# State


One issue you are going to face as you start modelling 'real world' things is there's a lot of 'near duplication' of semantic terms.

For example, modelling Lights you might end up with something like this:

* <code>on</code>: turn the light on /off - { write: true }
* <code>is_on</code>: is this on or off - { read: true }

Now consider a Denon Audio / Visual Receiver. It has, amongst other things:

* <code>on</code>
* <code>volume</code>
* <code>band</code>
* <code>mute</code>

So you end up with a parallel set of definitions

* <code>is_on</code>
* <code>actual_volume</code>
* <code>actual_band</code>
* <code>is_muted</code>

And when you're constructing user interfaces you end up having to figure out how to correlate all of these things, because it always takes _time_ for things to change. 
The period of time from when you issue a command to a Thing to when it actually completes the action is called the
**interstitial** state.

IOTDB went though this sort of thing for a while, but from a programmer POV it's kind of horrifying and doesn't quite seem right, as it's mostly a DRY violation.

What I ended up doing is creating the concept of a _role_, as in "what does this thing do", which can be one or both of iot:role-reading or iot:role-control

Now we just have 4 rather than 8 things to manage. "But how do you differentiate the _actual_ reading values from control values, as they're different?", you ask. 
