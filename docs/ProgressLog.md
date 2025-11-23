11/22/2025

Created base-repo for all of my code and to organize important documents, code
and everything else to keep my repo nice and organized. Everything is subject to 
change.

Also, went through and made a large overview and breakdown of how I am going to 
progress through this project. Milestones, objectives, making sure I am understanding
why I am doing the things I am doing -- and knowing how it all connects. Aiming to 
learn as I go and apply many different techniques to one goal. 

Got a list of all of my hardware that I have. Sensors, servos, small motors, nucleo board
and 3D printer. Focusing on making it all manageable to take on and do in small chunks.

11/23/2025

Working on python venv for GUI setup. Upgraded to 3.14.0 annd installed necessary packages
for everything I would need. 

Created venv: py -m venv env 

start script: env\Scripts\activate and just type "deactivate" for shutting off

pip install pyserial matplotlib numpy tk for all packages

Getting weird import errors, so I did pip list and made sure in my venv that packages
were appearing. Turns out VSCode needed to change the python interpreter to point at the 
python.exe from my venv folder. Got that fixed.

Created requirements.md for defining FR and NFR, project scope and objectives.