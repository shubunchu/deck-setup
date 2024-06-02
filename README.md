### Streaming setup

1. Follow the guide [[here](https://www.reddit.com/r/SteamDeck/comments/19ahzxq/youre_streaming_your_games_wrong_let_me_show_you/)] to set up Moonlight + Sunshine.

2. Follow the guide [[here](https://www.reddit.com/r/MoonlightStreaming/comments/rzpcpc/moonlight_streaming_without_monitor_no_dummy_plug/)] to set up a virtual display. This allows for us to stream games at 60+ FPS without having to keep our monitor awake. A video guide is [[here](https://www.youtube.com/watch?v=byfBWDnToYk)]. Edit the `option.txt` file to include the following entries:

    - `1280, 720, 90`
    - `1280, 800, 90`

    The Deck has a 16:10 aspect ratio (1280x800 native resolution), but not all games support this (e.g., P3R). In this case, we need to set up a supported resolution to fall back on (1280x720). The above entries allow for us to select a virtual display of 1280x720 and 1280x800 @ 90 Hz, respectively.

3. Download RTSS [[here](https://www.guru3d.com/download/rtss-rivatuner-statistics-server-download/)]. This software will allow for us to cap the FPS of our host to 90 FPS, optimizing our stream performance. After downloading RTSS, install rtss-cli [[here](https://github.com/xanderfrangos/rtss-cli/releases/tag/v1.0.0)]. We use this to programmatically access RTSS, and can automate the framerate limiting when establishing a stream connection (i.e., cap the framerate when streaming from Deck, and release the cap when disconnecting).

    1. After installing both, navigate to Sunshine (https://localhost:47990/).
    2. Within the header, select *Configuration*.
    3. Scroll down to the *Command Preparations* section. You should already have one command configured from Step 1.
    4. Select the *+ Add* button to include another command to run. Enter the following values for the newly-created command:
    - *config.do_cmd*:
        - `cmd /C "C:\Program Files\Sunshine\rtss-cli.exe" limit:set 90`
    - *config.undo_cmd*:
        - `cmd /C "C:\Program Files\Sunshine\rtss-cli.exe" limit:set 0`
    5. Select *Save*. Finally, select *Apply*. Sunshine will restart to utilize the configured changes.

### Additional resources + notes

- [[Steam Deck - Basic Use & Troubleshooting Guide](https://help.steampowered.com/en/faqs/view/69E3-14AF-9764-4C28)]
- You can add non-Steam games to Sunshine. We can review examples at [[here](https://docs.lizardbyte.dev/projects/sunshine/en/latest/about/guides/app_examples.html)]. Essentially, we can add the desired game as an executable to a new Sunshine application.
    - If you don't want to set this up, you can also simply launch Moonlight and run the *Desktop* application, and navigate to your game from there. You will need to change your controller settings to use the *Web Browser* template, such that we may use the touchpads to emulate mouse movement on our PC. Use `X` to open the virtual keyboard. After the game is launched, be sure to revert the controller settings to use the *Gamepad With Joystick Trackpad* template.
- Helpful shortcuts:
    - Terminate Moonlight session: `Select` + `Start` + `L1` + `R1`
        - Only use this if your stream is unresponsive. The game will still be running on your PC. Ideally, we want to exit gracefully, which can be done by closing the game through their respective menu.
    - Adjust brightness: `Steam` + `Left analog up/down`
    - Display Moonlight networking stats: `L1` + `R1` + `Select` + `X`
        - Useful for troubleshooting streaming issues. This can be used to determine if our bitrate needs to be lowered.
- Sometimes, you may find that your inputs are not working.
    1. In this situation, Select the `Steam` button. The running application will appear in the top-left hand corner.
    2. Select `Right` on the D-pad, and select *Controller settings*.
    4. Select *Controller settings* (should be highlighted by default).
    5. Under the *Current Button Layout* section, use the D-pad to select the *Using template:* option.
    6. Select `Down` on the D-pad, and select the *Gamepad With Joystick Trackpad* template.
    7. Press `X` to apply the layout. From here, you can select `B` to return to your game.
