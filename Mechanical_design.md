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

## The Slab ( V1 of drone ) 
Making the drone arms and frames for bottom and top were cool. But none of it will work if there is not a place for the microcontroller to be on.  


