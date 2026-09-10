# The Frame

## Initial Design (V1 of drone)

When first making the frame, I wanted it to be a medium-sized drone. More specifically, I wanted the size of the drone from one motor to the other side to be 14 inches, since the propellers' diameter was 9 inches. Hieght wise, I wanted it to be about 10 inches tall.
When first desighning the drone, I wanted it to be somewhat like a diamond shape, like racing drones. Bellow you can see that 
Figure 1 is what the bottom frame looks like while Figure 2 is what the top frame looks like. 
<table>
  <tr>
    <td align="center" valign="top">
      <img src="https://private-user-images.githubusercontent.com/226453623/648407851-b32a6b9d-3f1e-47d0-a008-822ec1d3a6a1.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3ODg5MzUzMjQsIm5iZiI6MTc4ODkzNTAyNCwicGF0aCI6Ii8yMjY0NTM2MjMvNjQ4NDA3ODUxLWIzMmE2YjlkLTNmMWUtNDdkMC1hMDA4LTgyMmVjMWQzYTZhMS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwOTA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDkwOVQwNjIzNDRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1lM2ZlMmY5NGU5NTEyYmYyNzVjYzJlNWY3YjNmMWVmOWQxNDM5OGRmMGIwNGE4ZjAxYjExODBkNmFiZDE2MTlmJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZyZXNwb25zZS1jb250ZW50LXR5cGU9aW1hZ2UlMkZwbmcifQ.vjVJMeMfWJsOwro8gF1fMMJw5oRW3mcGEz3VA5EigKs" width="100%" alt="Bottom Frame" />
      <br>
      <sub><b>Figure 1:</b> Bottom frame</sub>
    </td>
    <td align="center" valign="top">
      <img src="https://private-user-images.githubusercontent.com/226453623/648408915-eb662567-7b96-4313-8346-df5cf3119c1d.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3ODg5MzUzMjQsIm5iZiI6MTc4ODkzNTAyNCwicGF0aCI6Ii8yMjY0NTM2MjMvNjQ4NDA4OTE1LWViNjYyNTY3LTdiOTYtNDMxMy04MzQ2LWRmNWNmMzExOWMxZC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwOTA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDkwOVQwNjIzNDRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1kMWYzYmVlOGE0OGYyYmYwMTg4Y2M4ODhiM2VhNWNmNzIzYmRjNjAzODMyMjM4Y2Y5ZGRiNDA2OTNiMDI3M2QyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZyZXNwb25zZS1jb250ZW50LXR5cGU9aW1hZ2UlMkZwbmcifQ.r5M1ZqyD1JsKalKf1wSsaYVhAvMNldichW71RjQNauY" width="100%" alt="Top Frame" />
      <br>
      <sub><b>Figure 2:</b> Top frame</sub>
    </td>
  </tr>
</table>

When making the top and bottom frame, I had to think how would the drone arms fit to the  the top and bottom frame. I did this by implmenting multiple features for each bottom and top frame. For Figure 1:  
-  I did this by making for each corner 5 holes which would be screed in from top and bottom of bottom frame and top frame.
-  The 2 cirular holes which dont have a hole in them which look like they have some curvature in them are for the keeping the drone arms, flat bed for PCB to sit on and top frame all together using a tube.
-  The rectangular cutout was for teh PDB ( Power distribution board ) where it would take power from the battery and then feed to each of the motors, ESP32, IMU and reciver.

For Figure 2: 
-  There is no differnce from figure 1 except that the top is cut out so that more wieght can be saved and that components inside can be cooler when flyign around.

## The Drone Arms ( V1 of drone) 
Making of the top and bottom frames was easy but the drones arms was a whole challenge in itself sicne structurabilty, space, dimensions wirign for in drone arm were some problems I had to think about when desighing first. When I first started I intially thought 
of making built in arms where you would click them into the top and bottom frame but realized overtime that mechanism could break easily if not built right and wanted it simple. Eventually I went with the holes in bottom adn top of drone arm so it could be held tight 
with top and bottom frames. Then actually designing the drone arms was the challenge where first I made it using triables for the frame whihc worked out well. In figure 3 as you see, each of those lines on the top flange and all around were about .10 inches which are 
pretty thin. They did well against weight and teh arm was super light where it weighed about .10 pounds. Pretty light. 

<table>
  <tr>
    <td align="center" valign="top" width="50%">
      <img src="https://github.com/user-attachments/assets/4754ecca-db42-45b5-8525-0907cbeb8d77" width="100%" alt="Drone Arm View 1" />
      <br>
      <sub><b>Figure 3:</b> Drone arm design (View 1)</sub>
    </td>
    <td align="center" valign="top" width="50%">
      <img src="https://github.com/user-attachments/assets/1f66ac17-0892-4eaf-8310-76d3a63cf60b" width="100%" alt="Drone Arm View 2" />
      <br>
      <sub><b>Figure 4:</b> Drone arm design (View 2)</sub>
    </td>
  </tr>
</table>

<p align="center">
  <img src="https://github.com/user-attachments/assets/600a1c1f-76d3-4632-ae89-eb5f15f44ed9" width="70%" alt="Drone Arm View 3" />
  <br>
  <sub><b>Figure 5:</b> Drone arm detail</sub>
</p>

As you can see in Figure 3, using the triangles really helped since it was structurally strong with a reinforced center line to carry that stress; it helped. You can also see that near base leading up, ther is the smooth fillet which helpes reduce stress concentrations 
and all helps increase strenght. 
In Figure 4, I designed the motor housing to be like a cup so that in the event the drone crashed, it would hit the side of the frame instead of just the motor. 
Also, I made holes from the motor mount to the main body of the drone so that wires could easily go through the drone arm. 
Figure 5 shows how I left the back open so that there could be a lot of space for the ESC to sit and also for air to go through. I just made it big just in case something happened, while making sure that structural stability was still there. 

## The Fix for the holding the Slab ( V2 of Drone arm) 
When I made the first design of the drone arm, I realized that there is no holes or place for the slab to sit on. The slab is talked in the next bullet point but bascially, the slab is a place where the PCB sits which holds the microcontrolelr and other components needed for flyignthe drone. F

When tyring to quickly change the drone arm to fit the drone arm, I realized I also could redesign the drone arm again to be more more smaller while while almost keepign the same weight as V1 of drone arm. What I changed in V2 of the drone arm was make it more slender then V1 of drone arm and a more open design for the drone motor holding. As you can see across figures 6 - 8, the only thing I kept the same from V1 is the traingles on the side. Here are the main changes I made though for V2 of the drone arm. 
-  made the frame rods for around the drone arm .15 inches instead of .10
-  made the frame more traingular from a box shape in V1 of drone arm
-  made a hole near the drone motor mount so that wires has less stress instead of forcing them to go up like in V1 of drone arm
-  added a rectangualr hole at the bottom of the drone arm so that wires can easily be accesed if need be
-  made the insdie of the drone arm bigger realzing that V1 of drone arm was a bit small to acess wires. 

<table>
  <tr>
    <td align="center" valign="top" width="50%">
      <img src="https://github.com/user-attachments/assets/a1476004-eac1-41d0-911e-ad7a1cab42d6" width="100%" alt="V2 Drone Arm View 1" />
      <br>
      <sub><b>Figure 6:</b> V2 drone arm design (View 1)</sub>
    </td>
    <td align="center" valign="top" width="50%">
      <img src="https://github.com/user-attachments/assets/6f5773d6-833c-4c64-8a08-1e8a4d52b017" width="100%" alt="V2 Drone Arm View 2" />
      <br>
      <sub><b>Figure 7:</b> V2 drone arm design (View 2)</sub>
    </td>
  </tr>
</table>

<p align="center">
  <img src="https://github.com/user-attachments/assets/31670b1c-5d6a-4c90-b81f-8151292a89cd" width="70%" alt="V2 Drone Arm View 3" />
  <br>
  <sub><b>Figure 8:</b> V2 drone arm detail</sub>
</p>

## The Slab ( V1 of drone ) 
Having the drone arms and the frames is just one part of flying a drone. But how can it fly if there is no place for the microcontroller to sit on or be at in the frame, which is why I built the slab. This part sits in the middle of the drone, where the PCB sits. The PCB has the ESP32 and the IMU, which power the drone for flying. The holes you can see on the sides of the slab are basically what the slab sits on. When I made the first version of the drone arm, I didn't take that into account, which I then accounted for in the next version of the drone arm. It was a small alteration, but nothing major.

When first designing the slab, I made it in a hexagon shape since a circle or any other shape wouldn't work. As you can see in Figure 9, it fits very well. Along with making the slab, I also added holes to each of the sides to make sure it can sit on the holes of the drone arm. I also added depth for the slab, since when the PCB sits, there needs to be space underneath for the wiring and the solder underneath, which is why it is about .10 inches deep. Along with that, on the sides, I added slots on 4 out of the six sides, since if I ever need a wire or anything for the ESP32 or IMU sensor, that could work too. The last thing I had to add before this could all work was a hole through the part, since obviously, there needs to be some hole so wires can connect to the PDB at the bottom, which is what I did in Figure 10.

<table>
  <tr>
    <td align="center" valign="top" width="50%">
      <img src="https://github.com/user-attachments/assets/2a592202-6dfb-49ea-abab-49a7aee79dd5" width="100%" alt="Slab Design View 1" />
      <br>
      <sub><b>Figure 9:</b> Slab design (Side View)</sub>
    </td>
    <td align="center" valign="top" width="50%">
      <img src="https://github.com/user-attachments/assets/40d9c3ac-d119-4d11-8137-49bc77555895" width="100%" alt="Slab Design View 2" />
      <br>
      <sub><b>Figure 10:</b> Slab design (Top view)</sub>
    </td>
  </tr>
</table>

## The Landing Gear ( V1 of drone ) 

How will this drone land if there is no landing gear? My first inspiration came from helicopter landing gears, which have skids on them—static landing gears that absorb impact upon landing. I wanted to build those, but soon realized that by the time I was designing these landing gears, I had not built my first prototype together at all, so I tried to quickly within a day make a landing gear that would work, but would be crap. As you can see in Figure 11, it was very flimsy, but did the job of landing. I used a press fit for the pins at the top of the landing gear, where I had a .04-inch tolerance. A somewhat tight fit, but still a little loose. All I needed from this landing gear was that it would work and that it would not break upon impact. I tested this landing gear by dropping it from 5, 10, and 15 feet without the whole setup. It survived. Now with the whole setup at five feet, when I dropped it, there was a small crack. Seeing this crack, I printed 5 of these types of landing gears since they barely took any 3D filament. I knew that for V2 of the landing gear, it would have to be well thought out and way thicker and spread out to distribute the landing forces.

<table>
  <tr>
    <td align="center" valign="top" width="50%">
      <img src="https://github.com/user-attachments/assets/09c6e63f-d8f5-4956-add4-9585b0ffaedf" width="100%" alt="Landing Gear View 1" />
      <br>
      <sub><b>Figure 11:</b> Landing gear design (View 1)</sub>
    </td>
    <td align="center" valign="top" width="50%">
      <img src="https://github.com/user-attachments/assets/3bc030e1-2e43-4f0b-99cb-2971219cc3a9" width="100%" alt="Landing Gear View 2" />
      <br>
      <sub><b>Figure 12:</b> Landing gear design (View 2)</sub>
    </td>
  </tr>
</table>

## Putting Everything together ( V1 of Drone ) 

When I first put everything together, I was in awe. It was amazing. By this time, I still hadn't finished my code for flying the drone. I was about 85% done and knew there were going to be some software bugs, but I knew my frame for the drone was perfect. Little did I know there was impending doom and version 2 of the drone was desperately needed. You can see the full build of version 1 of the drone below.

<table>
  <tr>
    <td align="center" valign="top" width="50%">
      <img src="https://github.com/user-attachments/assets/0ed93fd9-9f44-4153-b8da-d6ddde3ca10d" width="100%" alt="Full Drone Build View 1" />
      <br>
      <sub><b>Figure 13:</b> Full drone build V1 (Isometric view)</sub>
    </td>
    <td align="center" valign="top" width="50%">
      <img src="https://github.com/user-attachments/assets/812278b4-3b19-4dc7-94a3-7b7de0c34bb2" width="100%" alt="Full Drone Build View 2" />
      <br>
      <sub><b>Figure 14:</b> Full drone build V1 (Top view)</sub>
    </td>
  </tr>
  <tr>
    <td align="center" valign="top" width="50%">
      <img src="https://github.com/user-attachments/assets/1e2d6871-4e80-49a4-bedf-d295c697e648" width="100%" alt="Full Drone Build View 3" />
      <br>
      <sub><b>Figure 15:</b> Full drone build V1 (Side view)</sub>
    </td>
    <td align="center" valign="top" width="50%">
      <img src="https://github.com/user-attachments/assets/7c672e4b-9acc-4a02-bfe5-99fd8c118f66" width="100%" alt="Full Drone Build View 4" />
      <br>
      <sub><b>Figure 16:</b> Full drone build V1 (Detail view)</sub>
    </td>
  </tr>
</table>









