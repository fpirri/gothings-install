# GoThings Raspi Install
How to install Raspbian and docker on a Raspberry board  
  
Get containerized HTTP server, node js, python and more on your raspi !  
<br />

ADVICE:
----  

**This project is under construction.**  

Project documentation is sparse and not reliable, owing to the on-going (re-)definition of many secondary aspects of the project.  
Owing to the above, please be aware it may be next-to-impossible to use this repository to make any useful work.  

Anyway, the original work included may be used according to the permissible MIT License.  

Please read the [disclaimer](#disclaimer) for more information  
<br/>

----
[What GoThings Raspi Install does](#what-gothings-raspi-install-does)  
[What you get](#what-you-get)  
[What you need](#what-you-need)  
[GoThings System short description](#gothings-system-short-description)  
[Pre-installation steps](#pre-installation-steps)  
[GoThings installation](#gothings-installation)  

[Disclaimer & Licensing](#disclaimer)  

----

<br />

What GoThings Raspi Install does
----  

* Lets you click/perform a sequence of actions to install docker on your raspberry pi board
* ***GoThings Raspi Install*** allows you to set locales, get some data from github and initialize the ***GoThings System***
* It runs a demo application
* It also install and execute the ***GoThings Control Menu*** on the board  
  
  
 ***GoThings Control Menu*** allows you to manage lifecycle of your containers
   
 ***GoThings System*** is an ensemble of cloud and embedded applications briefly described [below](#gothings-system-short-description")  
 
<br />  

What you get  
----  

   - docker installed in your raspberry pi (P1 & Pi Zero)
   - nginx running in your board as an HTTPS gateway to the external world
   - a basic HTTP service on-board
   - a NODE JS demo application you can modify
   - the ***GoThings Control Menu*** to manage your GoThings System

Through **GoThings Control Menu** you manage the lifecycle of all containers and user data in the *GoThingsSystem*

After that you may write your programs using javascript, python or PHP languages. They will each run in its own container.  

Please note the docker installation is a standard one. The *GoThings System* configuration data is made up from a few files and you may delete them and use docker for any other purpose.
  
<br />  

What you need
----  
  
* a raspberry P1-B+ or PI Zero W board
    * the procedure may work for other Raspberry board models
    * anyway, it is tested on P1B+ and Zero W boards only
* an sd-card to store the raspbian OS  
* an internet connection (you will download several big files)
    * you can download the OS from:  
          https://downloads.raspberrypi.org/raspbian_lite/images/  
        
* you have to follow the [PRE-INSTALLATION](#pre-installation-steps) procedure documented below to run the raspbian system on your raspberry *zero* board  
   
Finally, please follow the instructions in the [INSTALLATION](#gothings-installation) section below
 
<br />  

GoThings System short description  
----  

* The *GoThings System* is made up from a number of co-operating docker containers
* each container does a specific function but all the ensemble is seen from the network as a single entity
    * each container may use a different language, i.e. javascript, python, PHP, ...
* The *GoThings System* is made up from two parts: 'base' & 'user'
* The 'base' part gives to the GoThings System the capabilities common to most applications, such as network access and security  
* The 'user' part is specific to a particular configuration
    * please note: this part allows users to run their own code
* *GoThings* run in your Internet-of-Things, on the ARM achitecture boards such as the Raspberry Pi
* An alpha version of *GoThings* is now running in standard cloud virtual systems (It will be published ASAP [here](https://github.com/fpirri/gothings-cloud))

<br />

In [github raspi-apps](https://github.com/fpirri/gothings-raspi-apps")  you find:
* **GoThings Control Menu** to manage the lifecycle of your containers
* some templates that can be customized for specific purposes
 
<br />  

<br />  
 
### GoThings can be defined as:
##### a Docker Distributed Things Operating System (DDT-OS) running on a number of networked things.
  
GoThings uses nodejs, vuejs and python-flask technologies.  
GoThings networking is based on http protocol and exploits many of the nginx+lua+redis capabilities  
  
  
------------------------------

<br/>

## Pre-installation steps


- Choose your raspbian image.
   - the following instructions use:
       https://downloads.raspberrypi.org/raspbian_lite/images/raspbian_lite-2020-02-14/2020-02-13-raspbian-buster-lite.zip 
   - the first gothings release, archived [here](https://github.com/fpirri/gothings-raspi-install/tree/master/history/version-01), worked with raspbian-stretch lite version
   - You have to burn your sd-card to use it on the rasperry
   - if you wish to use a different release, please note that docker does not run on every armv6l raspbian images
 <br/>
 
Please note you have to abilitate SSH access on your raspberry in order to use the *GoThings System*  
To this end you may follow the official instructions or google 'headless raspberry setup' and choose one of the many tutorials.    
I successfully followed this [tutorial](https://styxit.com/2017/03/14/headless-raspberry-setup.html)  
You must also abilitate the wi-fi connection to use the *zero w* raspi model  
  
<br>
If it happens you use Linux on your PC, you can use the [zeroconf](https://raw.githubusercontent.com/fpirri/gothings-raspi-install/master/setraspiboot) shell script, following the instruction below.  
The script is tested with bash shell on ubuntu, it should run an many other linuxes.  
It may also run on *extended* MS Windows.  
  
The steps to follow:  
* download the (https://downloads.raspberrypi.org/raspbian_lite/images/raspbian_lite-2020-02-14/2020-02-13-raspbian-buster-lite.zip) raspbian image from the raspberry official site  
    * if you use [balena etcher](https://www.balena.io/etcher/) SD-card burning software you don't need to expand the zip archive  
* burn the *buster* image onto your SD card  
    * an 8GB card is required  
    * a 16GB or greater is recommended  
* inspect the burned card on your PC  
    * you should find two volumes: *boot* & *rootfs*
    * on ubuntu 18.04 it probably is /media/&lt;username&gt;/boot
      were &lt;username&gt; is your user name on the machine
* take note of the path of the boot volume
* download the setraspiboot script at https://raw.githubusercontent.com/fpirri/gothings-raspi-install/master/setraspiboot
    * open it in your editor
    * at the top you find 2 variables:
       SDBOOTDIR
       WPA_DATA
* update the script content:
   * your boot volume path in SDBOOTDIR
   * your wifi data in  WPA_DATA
   * you may add as many wifi network as you like
* save the script and launch it with the command:
     source setraspiboot
    * the script will run in your current environment
* eject the sd-card
* put the new card in the raspberry board and power it up
  
First time you should allow the board to complete OS installation.  
It may take up to a few minutes.  
You should see faint flashes of the LED, periods of darkness and finally the LED stably lit for more than 10 seconds  

At the end you can:
- Connect via ssh from a PC terminal on the same LAN
   - in terminal you can write:
   
        ssh pi@raspberrypi
        
      normally it automatically find the new board on LAN
      
   -  If that don't function please try googling 'find your raspberry IP address'  and connect via ssh from terminal:
        
          ssh pi@<your IP address>
          
          
- It is **VERY IMPORTANT** that you change your password to a very strong one ...

    -   **<-- PLEASE FOLLOW** this advice !!!


**You should now have a raspberry PI, reachable via ssh, which can run the GoThings System**
    
<br />

-------------------------------

<br />

# GoThings installation

<br />

#### 1- Connection
Connect to your board via ssh, commands below should be gived in the home directory /home/pi

#### 2- Download the 'zero' script
Exec the command:

      wget -O /home/pi/0 https://raw.githubusercontent.com/fpirri/gothings-install/master/0

The 0 (number zero) is the primary bootstrap script.
     
 To give yourself a minimum of security you should verify the integrity of the files you download from internet.  
To this end you have to calculate the checksum of the downloaded 0 file:  

       md5sum /home/pi/0  <-- you thype this
       54c6223a01420b9028720e9d5789adf3 /home/pi/0  <-- you see the locally calculated checksum

You should compare it with the file on github repository.
Content of github 0.md5 file is similar to:  
    
        54c6223a01420b9028720e9d5789adf3  /home/pi/0
        ---
        To evaluate the checksum above you may use the following command:
        md5sum /home/pi/0
        ---
        0  version 0.0.3
        ---
  
  
#### 3- Verify the 'zero' script
You should verify equality of the locally calculated checksum with that reported on the github repository

NOTE :  
  There are means of verification other than md5 checksum.
  Here MD5 is choosed because it is already available in the raspbian OS.  
 Security will be eventually improved later on

#### 4- exec the 0 script
Exec the command:

        . 0             <-- the command is:  'dot' 'space' 'number 0'

please note: this immediately executes the script locally, without the need to mark it as executable

#### 5- Install actions

 Follow the procedure suggested by the 0 script, one action at a time.  
**It is advisable to exec the first action only once.**  
You may execute the following sections multiple times, althought it should not be necessary.  
Last but one action dowload the  [g menu](https://github.com/fpirri/gothings-install "GoThingsControlMenu for things management") from github. It also allow you to exec the menu by typing './g' in the /home/pi/ directory.   
Anyway, Control Menu is not executed by this action, you should first verify its checksum after the download.  
Then, you may execute it by typeing ./g at the console.  


#### 6- Execution times
The execution time for each action is influenced by the raspberry board model and by the speed of your internet connection.  
Times below are for a raspberry P1B+ directly connected via LAN to a fast ADSL provider.  
Very similar times are obtained for the Raspberry PI zeroW board.

     A.1 First boot          :  4 m, including reboot;  
     A.2 Install utilities   : 7 m;  
     A.3 Setup user data     : less than 1 m;  
     A.4 Docker & docker-compose installation
                     docker  : 12 min;  
            compose  via PIP : 1h 15m;  
     A.5 Demo example
         images download : 32 m;   (first time only)
             run example : 2 m.  
         Note: this action can be safely interrupted and re-executed   
----------------------

<br /><hr />

# Enjoy docker !
-----


<br />

# DISCLAIMER
As commonplace in github, the project may include other work which may have different licensing terms.  
The author make his best to note usability and provenience of every work included here.  
A list of the software that inspired this work is reported in the [ACKNOWLEDGEMENT](https://github.com/fpirri/gothings-raspi-install/blob/master/ACKNOWLEDGEMENT.md) section.  
<br/>

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

Please consult the [LICENSE](https://github.com/fpirri/gothings-raspi-install/blob/master/LICENSE) section.

