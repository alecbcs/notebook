# Tricks for Better Battery Management

## Tools:

##### Powertop:

```bash
sudo powertop --auto-tune
```

## Intel Graphics:

###### /etc/modprobe.d/i915.conf

```bash
options i915 enable_guc=3

options i915 fastboot=1
```

## Audio Management

###### /etc/modprobe.d/audio_powersave.conf

```bash
options snd_hda_intel power_save=1
```


