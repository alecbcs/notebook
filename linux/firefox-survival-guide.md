# Firefox Survival Guide

## Use Xinput2 Events for Better Momentum Scrolling

By default Firefox reads the touchpad like a scroll 
wheel using xinput, then the gecko rendering engine also has some baked 
in smooth scrolling features to give a partial momentum scrolling feel. 
Personally I've always found this scrolling method to have a decent 
amount of lag and make Firefox feel a bit chunkier than chromium based 
browsers.

I found that if you set `MOZ_USE_XINPUT2=1` as an
 environment variable, Firefox can read xinput2 touchpad scroll events 
which allows Firefox to use the same momentum scrolling system that the 
Gnome apps use! There are a few different ways to set this environment 
variable but I did it by creating a `/etc/profile.d/` script.

```bash
sudo mkdir /etc/profile.d/

echo export MOZ_USE_XINPUT2=1 | sudo tee /etc/profile.d/use-xinput2.sh
```

And finally logout/back in! Hope this helps anyone looking for a more Gnome like scrolling feel in Firefox.



## Extensions:

- **Multi-Account Containers**

- **Temporary Containers** (Allows you to create a throwaway environment for most web browsing and then on pages you want to save logins for use manual account containers to always open that website in a permanent container.)

- **uBlock Origin**



## Fixes

#### Enable Layers Hardware Acceleration to Fix Screen Tearing

On many systems I've experienced screen tearing in videos and animations. Setting `layers.acceleration.force-enabled` to true in `about:config` almost always fixes it for me.


