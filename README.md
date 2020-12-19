# How to keep music out of your Twitch VODs

Twitch recently added the ability to have two different audio tracks in your stream, one for the live stream itself and one for the VOD/clips. You can use this to keep music out of your VODs as a layer of protection from DMCA strikes. For example, if you get permission from an artist to use their music on your stream, and they later sign to a major label, that label might DMCA your VODs! Even if you'd win in a theoretical court case, it would still be a problem for your Twitch account. By not including music in your VODs and clips, you avoid this situation.

This is a guide to setting that up in a reasonably simple way on a single PC running Windows. If you have a separate stream PC or you're already pretty much an expert with an audio mixer, you might not need most of this guide (maybe just skip to the last section about OBS configuration to learn about the actual new stuff).

First, get the following software:

1: OBS Studio 26.1 or later. I am unsure if streamlabs OBS supports this feature.

2: Voicemeeter Potato. Unlike most software that asks you to restart your computer, after installing Voicemeeter you really do need to restart for it to work. ( https://vb-audio.com/Voicemeeter/potato.htm )

3: If you're on a version of Windows older than 10, you need audiorouter. Windows 10 has this functionality built in. ( https://github.com/audiorouterdev/audio-router/releases )

The way this is going to work is we will have your audio split into three streams: your mic, your music, and your game audio. Those streams will all go into Voicemeeter, and from Voicemeeter into OBS and also your headphones. The main thing making this need to be so complicated is that you can't use your normal "desktop audio" source in OBS anymore, because it's going to contain the music you're listening to mixed with your game sounds, and those need to be separated. 

It's not strictly necessary that your mic goes through Voicemeeter, but doing so will allow you to apply useful effects to your mic, so if you're going to all this trouble you might as well hook that up while you're at it.

## Step 1, Voicemeeter Configuration:

Open Voicemeeter, and make it look something like this: https://i.imgur.com/u55l2Db.png

I have circled the relevant things in red. 

A1 is your headphones. B1, B2, and B3 are outputs that will go to OBS.

On the far left is your mic. Click on the name up top and you'll get a list of devices. Select the one named like "WDM: your brand of microphone". At the bottom, set it so it's sending only to B1.

In the middle are three virtual inputs. We're using the left two of them. These will be your desktop audio and your music. Set them both to send to A1, the left one to send to B2, and the middle one to send to B3. (You can see at the top I have named them "Desktop" and "Firefox". You can rename yours with right click if you want to.)

In the top right, click A1 and make sure it's set to the WDM version of the headphones you want to hear game audio and music coming out of.

You might have noticed I have a device at the middle left called "Line In". This is for when I'm streaming a console game with the audio plugged into the back of my PC. If you don't do this, ignore that part.

Optional: click A1 by your mic to hear yourself talk, then play with the built-in "intellipan", compressor, noise gate, etc to see if you like what they do to your voice.

## Step 2, Audiorouter/Windows Configuration:

Figure out what program you want to play music from. (e.g. Spotify, Firefox, Winamp, whatever.) We're going to send audio from this program to a special Voicemeeter input.

If you're on Windows 10, right click the taskbar speaker icon and do "Open Sound settings". Scroll down and click on "App volume and device preferences". Find your music program and set its output to "VoiceMeeter Aux Input (VB-Audio VoiceMeeter AUX VAIO)"

If you're not on Windows 10, open Audiorouter. Find your music program, click the arrow at the bottom, click "Route", and select "VoiceMeeter Aux Input (VB-Audio VoiceMeeter AUX VAIO)". You will have to repeat this step each time you start your stream, or never close audiorouter.

## Step 3, Windows Configuration:

Press the windows key and type "manage audio devices" to open the audio devices window. In the Playback tab, find the entry called "VoiceMeeter Input (VB-Audio VoiceMeeter VAIO)", right click it, and select "Set as Default Device". This will make all the audio from any games or other programs go into Voicemeeter. For times when you're not streaming, you'll need to either keep voicemeeter running 24/7 to handle your audio, or you'll have to toggle this setting back and forth between Voicemeeter and your actual speakers every time you turn on or off your stream. 

You should now test this part of the setup. In Voicemeeter, do "Menu -> Restart Audio Engine" (also do this if Voicemeeter ever seems to freeze up.) The three audio meters in the lower right should now have your mic, your game audio, and your music. Make all three kinds of sounds happen and verify that they're showing up. You should also hear the correct audio in your headphones.

## Step 4, OBS Configuration:

In OBS, go to Settings -> Output and check the boxes for "Enable Advanced Encoder Settings" and "Twitch VOD Track (Uses Track 2)". Then click into the Audio tab on the left, and set the three Mic/Aux dropdowns to the three Voicemeeter outputs like so: https://i.imgur.com/QZpBDTw.png (these are B1, B2, and B3 from inside Voicemeeter)

Hit OK, then right click in the OBS audio mixer and do "Unhide All" to make sure the three new sources are visible. Rename them something appropriate like mic, music, and desktop audio. Disable any other audio sources. Then right click in the mixer and go to Advanced Audio Properties. Make it look something like this: https://i.imgur.com/4Q3tW2D.png

The important part is on the right. Each audio source has 6 checkboxes that can be used to include it in tracks 1 through 6. Track 1 is what's played on your live stream. Track 2 is what goes in your VOD and clips. Tracks 3 through 6 are irrelevant. You want all three of the sources we configured to go to track 1, but have music not go to track 2.

You're done! There's nothing you have to do on Twitch's website itself, but you probably want to do a test stream and verify that the correct audio is going to the correct places.
