**RFID Lockbox**

Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Xinkun L. | Canyon Crest Academy | Electrical Engineering | Incoming Junior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your second milestone, explain what you've worked on since your previous milestone. You can highlight:
- Technical details of what you've accomplished and how they contribute to the final goal
- What has been surprising about the project so far
- Previous challenges you faced that you overcame
- What needs to be completed before your final milestone 

# First Milestone: Finish Building The Circuit And RFID Tag Reader

<iframe width="560" height="315" src="https://www.youtube.com/embed/ur9CDYwbdSo?si=tKRHFVfpNjszn-9u" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


During my completion of the first milestone of this project I have used female to male wires, jumper wires, resistors, RFID reader, LEDs, arduino board, a solenoid, and Arduino IDE to code the functionality of the circuit. The wires I used to connect the circuit and the RFID sensor alongside the LEDs and the solenoid so that through the code the right RFID tag will activate and deactivate the solenoid, which will later allow for the opening and locking of the lockbox. The LEDs shows if the tag is the correct one or not through the use of the red LED indicating it not working and a green LED indicating it does. They will eventually fit into the case of the actual lockbox which I will make out of cardboard to start with. Due to my little experience with arduino as a whole and most of the items such as the RFID sensor and the solenoid I have had to search up what they do, guides on how to wire them, and guides on how to actually upload the code and how to make the code in the first place. For the code I currently have in my arduino it is something I used from another creator and modified to work with my solenoid. Most of my challenges came from the inexperience of using such materials, but I was able to overcome that through research and testing as well as asking for help on some parts. My milestones had to change from finishing the coding and circuit being milestone 2 to it being milestone 1 and making the box/case milestone 2 instead of milestone 1. I plan to integrate the circuit I have made so far into the lockbox I will make in the future and make modifications from there including changes to code or physical changes. One of which include making the card reader a sort of slot where if you have the incorrect card it will keep the card inside the slot and keep it and if it is correct it will send it out through a motor.

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("Hello World!");
}

void loop() {
  // put your main code here, to run repeatedly:

}
```

# Bill of Materials

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Solenoid | Used For Locking Mechanism | $9.99 | <a href="https://www.amazon.com/KEYESTUDIO-Electromagnet-Module-Arduino-Environmental-Friendly/dp/B07H3V8N2Q/ref=sr_1_1?crid=38H9YUJM1HGCB&dib=eyJ2IjoiMSJ9.RclhSvYDt3GTcdVF0kHRfLERSn4LCrPjuWOFO1S-VACfr5d82it1eJF1CqnUBd8va2q3sAgfx-5zctuQ6QG5gRWzxarWa7mmLc8BGuv72x7Rs3tnw-cKuvTyEILGjwv3qH3W_W8ebRYuJdkb25AH-yS__Ll659TRIFe602Y5ar_kh0vWW8Mw8A3rzgjqmXdUHW_lQ3b8xYNd8CUhxsgZ8YYQdrsqkuD04JVoR-RAIAq1Gp-yCpaXpV9QUoPm7_u2pV4Z_QufMD_k91GGoP6lwgQDkl9OtI4BsLQUs2CmckY.KOMmGAfeUR0ckcABdw0Uynk8P8vlFi48B1j_wMFKv3k&dib_tag=se&keywords=keyestudio+solenoid&qid=1784666814&sprefix=keyestudio+solenoid%2Caps%2C201&sr=8-1"> Link </a> |
| RFID Kit | Used As The Opening And Closing Activation Mechanism | $9.99 | <a href="https://www.amazon.com/HiLetgo-3pcs-RFID-Kit-Raspberry/dp/B07VLDSYRW/ref=sr_1_3?crid=YTSQKHJFAM0F&dib=eyJ2IjoiMSJ9.Vrq1EZl16S8bS7qWKOC5T46uD51TlM2aSO1lnCW8zUtR5MG3W6mcLV9jwan178gp0FznllES5qZsWkriTEgh8Sb-LlPOBLHZeGbbjYa9rZw-IAihnI-5tmdGEfnRnv29ut0go6p9f2ar_hyTg70KVO-rqb5EqzImfOqdZT7PjWM1RBlJRwIwePi-T9VrMiexhwlRg2i66GmTpyoKGu7fNVT2ttKlRgyyyOS6YTeW7kTJW_uhgXpl8FbLepBh4W9lb6ay1xNO_vcvvCNCPl8tOBL1qRoqb51-S38KGmN6ZMc.8smbr607SVSyLmPx87gUL0e_33-rdhqdBhHWyShIeCM&dib_tag=se&keywords=Rfid%2Bkit&qid=1784751861&s=electronics&sprefix=rfid%2Bkit%2Celectronics%2C475&sr=1-3&th=1"> Link </a> |
| Magnets | Used For Mechanisms In The Lockbox | $3.99 | <a href="https://www.amazon.com/Towjug-Adhesive-3M-Anisotropy-whiteboards/dp/B0CQLHFSGF/ref=sr_1_4?crid=3SKTFJWJNTA7F&dib=eyJ2IjoiMSJ9.u9nAZouZDsHRy4xSbvQmX4RJYps3uPDKnSs7qhfQW62g7IEV44QOiwxxsbMyuGcHo_jI8N0vWUpKC0mVH_vRmi_QOTKoqoMyg1tuxdqNZTE_Kv9E-MHfc2ptZR6lPcqMCfUwewrCjo_ZEldI6a46BgVAb5NO9UaaZzN-0v0saFTbsmQFCEOt4mznza-99d8SMBgXl_vIDMUrn662tYdGgNNaz85eFGqgC3Y3ewixZKg.FPi507YlOlZqTYaH0yHR-BvmPiCeVTva6Hr_19TowG0&dib_tag=se&keywords=magnets+for+crafts+science+projects+20+pieces&qid=1784667136&sprefix=magnets+for+crafts+science+projects+20+pieces%2Caps%2C179&sr=8-4"> Link </a> |
| Cardboard | Used To Make The Physical Lockbox | $7.99 | <a href="https://www.amazon.com/Corrugated-Cardboard-Inserts-Shipping-Mailing/dp/B0GSJ7K4G7/ref=sr_1_9?crid=16V3AITL4GCJ&dib=eyJ2IjoiMSJ9.xximf4qVenL0nm7v5zeOL3xXoaFPr3ZoFcphdDjOAbq3-MRxf9IWvFO7ozaeWC1uWA9t_4-gbVKJ5DiGwePTI434QIue9yP47wswK2D4-F-Gq77YbhMQ81NNUQsgMEXUMMyUIHp2TlM-HdVufOsN9qbRdBdcuFhDcozF1ew_5zdW1UrhQKBxuMkzCuGbqF4mTo-RqhhpvpQbW7z_3IpkdIOUdb0neqaMUtE7w0zN4KQ.Rr5N3zN5f48tsytgo-udlpovR-IRAnEGeK4wen9bt9g&dib_tag=se&keywords=cardboard&qid=1784751508&sprefix=cardboar%2Caps%2C276&sr=8-9"> Link </a> |
| Digital Multimeter | Debugging The Circuit | $9.98 | <a href="https://www.amazon.com/Multimeter-Voltmeter-Continuity-Resistance-Electrical/dp/B0CXM242J1/ref=sr_1_8?crid=2HWKZQ1L9UFMT&dib=eyJ2IjoiMSJ9.YVNSL1xVjC5yYKka0_czm3XIzjU9qm2oiKy4tFo2urlFqhI9RS5-BYAA4NR4orfjE1D2FK8THK5AhKySZ3uSccZWQrTqNTZuUHW22VVvki6ULiqF1_0OEVc97fhCWFgsl5Mlu3jb7whwE545hTr7npY1DTA7xWOVrwEyNEC4k13IXl17WVdT538kh0XAu0e-jrz7gEMeehzKUwSgaaPopZVMFbRSDbqTWK5WWaJ_qVjWsGFllf1GjtLfohry_IrzaJjajYA_VkvJRyxfvjXj3Ebu_dHxSXY420sIbmwBkOM.iX5A0tqbNUa8ZR-BN7i6EPJoP_GyuW8m_JR5KCWy8r0&dib_tag=se&keywords=digital+multimeter&qid=1784667203&sprefix=digital+multimeter%2Caps%2C291&sr=8-8"> Link </a> |
| Uno R3 Project | Used To Create The Circuit | $59.99 | <a href="https://www.amazon.com/EL-KIT-001-Project-Complete-Starter-Tutorial/dp/B01CZTLHGE/ref=sr_1_1?crid=6U2NHMIRHWTJ&dib=eyJ2IjoiMSJ9.-TMWe7jTY1L2k9FBx9xn4xCdT24tTazF2-SXFdY8Xs_Dlt_Mw9l1ut8CxifbBzmK8OBAZrlxa_Ywy5wmPctCJw1xVljPsyd1_230rfPpc4QPnWEnEusheDWOR7nF5pkcHdGBP6tW2s7VdqQj9TvwFdikvcVUyub8E_2RvaOxoQv0ToZcPQQf3CzARWAIdm9AgM4Jq_tkEF-_qCHBWOqaaV6VHGrPF8LbtyLHLtLG7rk.6XUVfbZRZg3RssKm40WDNMEiq6GhmxtxamoH67YmEWo&dib_tag=se&keywords=Uno+R3+Project&qid=1784667365&rdc=1&sprefix=digital+multimeter%2Caps%2C326&sr=8-1"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

# Credits
- https://www.youtube.com/watch?v=_9unR083OPY
- https://kitronik.co.uk/blogs/resources/arduino-based-rfid-box-lock
- https://the-diy-life.com/arduino-based-rfid-door-lock-make-your-own/
