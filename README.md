
# ES-DE to KWGT sync

This page contains instructions on how to sync game navigation in ES-DE to a KWGT widget through Tasker in order to create a dynamic wallpaper. This allows more cosmetic freedom for dual screen devices like the AYN Thor. Normally this type of wallpaper functionality should be done through KWGT's more powerful brother, KLWP. However, the AYN Thor does not let you assign KLWP to the bottom screen hence why I came up with this workaround.

I would only recommend trying to set this up if you strongly prefer ES-DE over other launchers that have native dual screen support and you want to use ES-DE primarily on the top screen. KWGT is not intended at all to be used as a wallpaper and that comes with downsides:

- The sync can be unresponsive (generally taking around 1 second, at times taking up to 2 seconds)
- You can't fade from one wallpaper to the next, it will simply swap
- Widget placement and sizing is finicky to say the least

Don't proceed unless you're okay with an imperfect solution that requires tinkering. I also want to make it clear that I'm no expert with any of the apps used. There are probably easier or more optimised ways to do this. Plus, you'll likely have to make manual adjustments in Tasker and/or KWGT. I'll provide some instructions but not a full on tutorial for those apps.

# Requirements
- [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm) (paid app)
- [KWGT](https://play.google.com/store/apps/details?id=org.kustom.widget) (pro version required to import presets, but you can do it manually on the free version)
- [Smart Launcher](https://play.google.com/store/apps/details?id=ginlemon.flowerfree) (I believe the free version supports widget resizing, but I'm not sure)
- [ES-DE](https://www.patreon.com/cw/es_de) (paid frontend)

I will assume you've already setup ES-DE on the top screen and Smart Launcher on the bottom screen.

# Instructions

1. Go to the main menu of ES-DE, Other Settings and make sure "Enable Custom Event Scripts" and "Browsing Custom Events" are both on.
   
   ![](/img/esde.png)
   
2. Now take the scripts folder from the Files in this repository and copy it to the ES-DE folder on your device. This should give you an "ES-DE/scripts/game-select" folder with the game-select.sh script in it.
3. The script itself is very simple. All it does is write to a few text files in the Tasker folder with the path to the selected game, name of the selected game and system.
4. Copy the Game_Selection_Scroll.prf.xml from this repository to the "Tasker/profiles" folder on your device. If you haven't used Tasker or made a profile before, this folder might not exist yet.
5. Just in case, run ES-DE with the scripts in place and scroll through some of your games. This should generate the esde_game_scroll.txt that we'll be working with. It should be in the Tasker folder. 
6. Open Tasker, tap on the profiles tab to get a submenu, select "Import Profile" and then select the xml file you just downloaded. Also, Tasker needs all sorts of permissions to work properly. It should ask for these on its own if it doesn't have them already.
7. After importing, you should see the "Game Selection Scroll" profile in Tasker. Make sure the toggle to the right of the profile is active. Now on the left click on "File Modified Tasker/esde_game_scroll.txt". Then click on the magnifying glass next to File and make sure it points to the txt file we just generated above.
    
  ![](/img/taskerfilesel.jpg)

8. Back on the profile screen click on "Change BG Selected", you'll see the steps Tasker will execute whenever you navigate to a different game.
   
  ![](/img/taskeroverview.jpg)
  
9. This is where I did some gross hardcoding. I might change it to a more general solution in the future. In step 4 of the task, Tasker will split the path to the game on every "/". If your folder structure has the same amount of steps as mine, that path and the split results will look something like this:
   
   ![](/img/taskerpath.jpg)
   
   The only ones relevant are ESDEselected6 and 7. AKA the system folder and game file. If your path to the game file is longer or somehow shorter, you need to make changes to step 5 and 7 of the task to adjust for this. Click on step 5 in the task.
   
   ![](/img/taskerstep5.jpg)

   Change the number at the end of "%ESDEselected7" to however many steps deep your game file is. Literally just count the amount of "/" in your path + 1, and then adjust the 7 based on that. Afterwards, open step 7 in the task overview and click on the pencil icon
   
  ![](/img/taskerstep7.jpg)
  
  ![](/img/taskerstep7v.jpg)

  The string at the top points to the ES-DE directory containing the image we'll be sending to KWGT
  - First change the numbers of ESDEselected6 and 7 here if needed.
  - Secondly, if ES-DE (and the downloaded_media folder within) are located somewhere else, you'll have to adjust the whole path. Mine assumes that ES-DE is a root folder on internal storage.
  - Also, if you wish to use something other than fanart, you'll want to change the directory in this path as well. Boxart is in the "covers" folder, the mixed art is in "miximages".
  - The fanart by default seems to be jpg, but the others are png's. So double check the file extension required for your images of choice, if you need to change it from jpg go back and adjust step 5 again but this time change the value under "Replace With".
  - Make sure to save all the changes. Go back to the profile overview/main screen of Tasker and click the save button there too.

  10. Add a Kustom widget to your page in Smart Launcher. If you want to have buttons or other widgets on top of the wallpaper, you'll want to set all of those up first. It's pretty painful to adjust afterwards.
  11. Click on the widget to go to KWGT. Import the preset from this repository there (if you have pro) or build the widget yourself. If you're doing the latter, simply add an image item and give it the formula below. You can add a formula by clicking on the square next to bitmap and then the calculator at the top.

  ![](/img/kwgtimg.jpg)
  ![](/img/kwgtimgf.jpg)

  Either way you'll likely have to come back to this to change the sizing and centering depending on what you want the end result to look like. If you also want the text displaying the game title and system, the formulas are below. The preset already includes these.

  ![](/img/img/kwgttitle.jpg)
  ![](/img/kwgtsystem.jpg)

  12. Now you just need to place and resize the widget to fit your vision. Honestly, this is the worst part. These instructions will assume you want a fullscreen wallpaper. Smart Launcher thankfully lets you freely resize the widget. Click Fine positioning and try to get it to fill the screen.
      
  ![](/img/sl.jpg)

  Then click Resize to further adjust it
  
  ![](/img/slresize.jpg)

  For a screen filling wallpaper I use these values, but you'll probably have to make some adjustments. It's really finicky.
  
  Target side left: X -0.36
  
  Target side top: Y -0.37
  
  Target side right: Width 7.91
  
  Target side bottom: Height 6.80
  

  After you're done, double tap the wallpaper and KWGT will auto adjust the image size. This is the part where you pray that it ended up well. If not, you'll have to either go into KWGT and play with the sizes and centering of the image there, or you'll have to adjust the widget sizing values above. Experiment.

  At this point everything should work in unison. You might want to lock Smart Launcher once everything is set up to your liking. It's very easy to move the widget by accident and you'll have to do the resizing all over again.
  
# Issues 

- When you go back from the games list to the systems overview, the wallpaper stays on the last selected game until you navigate to another game. There's no good way to reset to a "default" wallpaper. The only solution I've found for this induces major stuttering to the system view.
- Responsiveness. I think this is simply the downside of having to use KWGT. If someone figures out a way to use KLWP on the bottom screen of the AYN Thor, the sync would likely be more responsive. I've added a 750ms wait time to the task to at least make the speed of swapping feel a bit more consistent.


