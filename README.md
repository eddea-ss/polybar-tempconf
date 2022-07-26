# polybar-tempcore-config
 Fix and config temp core (bspwm) polybar in archcraft linux system
![image](https://user-images.githubusercontent.com/14878867/180899078-b3769402-92ee-4b29-83ac-229483e4d8e3.png)


-------------------------------------------------------------------------
Show resourses used in your machine temperature and porcentage cpu, ram
Fix and config (bspwm) polybar in archcraft linux system
-------------------------------------------------------------------------

Comands for bash terminal

- 1 - Go to your polybar directory, in my case:

   $ cd ~/.config/bspwm/polybar/
   
   
   

- 2 - Test running the bash code "scripts/temp.sh" in your terminal

   ***** start code in bash ****
   
    $ sensors | grep -m 1 Core | awk '{print substr($3, 2, length($3)-5)}' )
    
   ********* end code **********

   *note:*
   
   if its not work, maybe you need install lm_sensor on your distro:

      ---------------------------------
      In arch system:
         $ sudo pacman -S lm_sensors
      or:
         $ sudo yum install lm_sensors

      ---------------------------------
      In debian:
         $ sudo apt install lm-sensors

      ---------------------------------
      In fedora:
         $ dnf install lm_sensors

      ---------------------------------

   *note:*
   
   if you want, you can install other sensor package.
   but you need change the bash code in "scripts/temp.sh"



- 3 - Open file "modules" on your polybar directory and insert module temp:

   $ nano modules
   
   ***** add in end file *****
   
    ;----------------------------------
    [module/temp]
    type = custom/script
    interval = 0.5
    thermal-zone = 0
    exec= sensors | grep -m 1 Core | awk '{print substr($3, 2, length($3)-5)}'
    units = true
    format = <ramp> <label>
    label = " %output:0:15:%"
    ramp = 
    ;;--------------------------------
   
   ********** end file ***********



- 4 -  Add your module in "config" file:

   $ nano config

   ****** insert where display module-[left, center, right] *****

   $ modules-center= temp cpu memory

   ***********************************

   *note*
   
   if you have other modules in "modules" file, you can add in this part

   for example:

      modules-left = bspwm sep sep cpu sep memory sep temp
      modules-center = mpd
      modules-right = volume sep backlight sep network sep battery sep 202
   
   I will leave in repo the modules that are configured in archcraft by default


- 5 - Reset polybar

thanks to denysvitali for the solution, and to archcraft for the created modules

- deny repo
https://github.com/denysvitali/polybar-config.git

- archcraft oficial website
https://archcraft.io/
