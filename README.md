# ES-DE to KWGT sync

This page contains instructions on how to sync game navigation in ES-DE to a KWGT widget through Tasker in order to create a dynamic wallpaper. This allows more cosmetic freedom for dual screen devices like the AYN Thor. Normally this type of wallpaper functionality should be done through KWGT's more powerful brother, KLWP. However, the AYN Thor does not let you assign KLWP to the bottom screen hence why I came up with this workaround.

I would only recommend trying to set this up if you strongly prefer ES-DE over other launchers that have native dual screen support. KWGT is not intended at all to be used as a wallpaper and that comes with downsides:

- The sync can be unresponsive (generally taking around 1 second, at times taking up to 2 seconds)
- You can't fade from one wallpaper to the next, it will simply swap
- Widget placement and sizing is finicky to say the least

I also want to make it clear that I'm no expert with any of the apps used. There are probably easier or more optimised ways to do this.

# Requirements
- Tasker (paid app)
- KWGT (pro version required to import presets, but you can do it manually on the free version)
- Smart Launcher (I believe the free version supports widget resizing, but I'm not sure)
- ES-DE (paid frontend)



# Issues 

- When you go back from the games list to the systems overview, the wallpaper stays on the last selected game until you navigate to another game. There's no good way to reset to a "default" wallpaper. The only solution I've found for this induces major stuttering to the system view.
- Responsiveness. I think this is simply the downside of having to use KWGT. If someone figures out a way to use KLWP on the bottom screen of the AYN Thor, the sync would likely be more responsive


