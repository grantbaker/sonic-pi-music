# sonic-pi-music
Music I've made using [Sonic Pi](http://sonic-pi.net/). Mostly for fun when I have time.

## Song List:
- Set Sail (in progress)

### Other songs I've made without Sonic Pi:
All of these songs were made in 16-bit with [nanoloop](https://www.nanoloop.com/).
- [Set Sail](https://www.youtube.com/watch?v=urAHMMf_SKE)
- [Silver Spark](https://www.youtube.com/watch?v=zcN7HqGbNjE)
- [Vale](https://www.youtube.com/watch?v=wQ52D_f8I2k)

# How I got Sonic Pi working on Ubuntu Studio with PulseAudio
I have a MSI GS60-002, and its sound card doesn't play well out-of-the-box with Sonic Pi or JACK. I installed [Ubuntu Studio](https://ubuntustudio.org/) 18.10 and installed [Sonic Pi](http://sonic-pi.net/) from the Ubuntu repositories with `apt`.

I found that Sonic Pi didn't finish startup because it was looking for a JACK server. I started one with `QjackCtl`, but that disabled PulseAudio from working and I still couldn't hear anything from Sonic Pi.

The solution was using [Cadence](https://kxstudio.linuxaudio.org/Applications:Cadence), which I installed by using KXStudio's repository `.deb` and using `apt`. I had to change the following settings:
- Configure --> Driver --> change Input Channels and Output Channels from 0 to 2
- JACK Bridges --> ALSA Audio --> Bridge Type: "Alsa -> PulseAudio -> JACK (Plugin)"
- JACK Bridges --> PulseAudio --> Start + Auto-start at login

The result had audio from both Pulse and JACK playing out of my laptop speakers and 3.5 mm. To solve this, I used `alsamixer` to disable the laptop speakers. However, the 3.5 mm had line level coming out (i.e. really loud for my headphones). This behavior is expected since JACK is intended for use in a professional audio environment. This can be solved elegantly by using a different DAC, or what I did was plug in my Denon stereo receiver, disable speaker output, and plug my headphones into the 1/4" jack on the receiver. This way, I could use my receiver to adjust the volume of my headphones to a reasonable level (and gave me the ability to adjust the EQ!).

TODO: MIDI

