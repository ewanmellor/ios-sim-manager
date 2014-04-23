ios-sim-manager
===============

A state manager for the iPhone Simulator on Mac OS X.  This can save and
restore the simulator state, so that you can repeat tests from a known state
(or whatever).

# Example session

```
$ sim list
$ sim save my-first-state
Copying iPhone Simulator/7.1/Applications/3C1D4A74-6B89-41B4-85F9-0BB59A66BD3B to MyApp/my-first-state... done.
$ sim list
my-first-state:  156M

$ # Do some stuff in the simulator

$ sim save my-second-state
Copying iPhone Simulator/7.1/Applications/3C1D4A74-6B89-41B4-85F9-0BB59A66BD3B to MyApp/my-second-state... done.
$ sim list
my-first-state:  156M
my-second-state:  123M

$ sim restore my-first-state
Copying MyApp/my-first-state to iPhone Simulator/7.1/Applications/3C1D4A74-6B89-41B4-85F9-0BB59A66BD3B... done.

$ sim rm my-first-state
Are you sure you want to delete my-first-state? [yN] y

$ sim clean
Are you sure you want to delete all saved simulator state? [yN] y

$ sim pwd
/Users/ewan/Library/Application Support/iPhone Simulator/7.1/Applications/3C1D4A74-6B89-41B4-85F9-0BB59A66BD3B/MyApp.app

```

Note that the app inside the simulator is selected based on time.  The last
app that you installed is the one that's going to be copied to / from.  The
idea with this is to fit in with an Xcode workflow where you're building
and running whichever app you're currently working on.

# Installation instructions

The app's official name is ios-sim-manager, but you may want to use a shorter
name.  I use "sim", as you can see from the example session above.

```
# If you don't have a ~/bin directory already:
mkdir -p ~/bin
echo 'export PATH=~/bin:$PATH' >>~/.bashrc
. ~/.bashrc

IOS_SIM_MANAGER_DIR='wherever you cloned this repo'
ln -s "$IOS_SIM_MANAGER_DIR/ios-sim-manager" ~/bin/sim
```

# Credits

ios-sim-manager is by Ewan Mellor.

It is is heavily influenced by Musical Chairs by Orta Therox & Art.sy
(https://github.com/orta/chairs) except:

1. I found their push/pull terminology confusing, so I'm using save/restore instead;
2. I did not like the fact that it put the state in a subdirectory in your
source repo because that made recursive grep miserable, so state is stored
in ~/.chairs instead;
3. it's written in 200 lines of bash, not 600 lines of Ruby.

# License

ios-sim-manager is MIT-licensed.  See LICENSE.  Have fun.
