# Automatic irrigration and plant watering system
Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Makayla L | Chaparral High School | Electrical Engineering | Incoming Junior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

[![Watch the video](https://img.youtube.com/vi/Nn2hlWvWxzw/0.jpg)](https://youtu.be/Kht8bXbPvfU?si=4uK_B3hxmdJG1pcP)


In my final milestone, I implanted additional sensors to better monitor the plant’s environment. I incorporated temperature, light, humidity, and rain detection all onto the LCD. Additionally, an automated fan was added to regulate the temperature, in case of any overheating. Throughout these 3 weeks, I spent working on smart Irrigation, I found the most difficult in my last milestone, setting up the photometer, as there were no instructions provided, and I had to greatly modify the code to get the photometer to correctly detect light. I learned how to research efficiently and work diligently. I enjoyed wiring and building my first engineering project, so I plan to continue with Arduino and create additional projects to gain more experience. 



# Second Milestone

[![Watch the video](https://img.youtube.com/vi/Nn2hlWvWxzw/0.jpg)](https://youtu.be/J8xkz_8wU8k?si=DI6O8Y7e5TF3kY4R)


In this milestone, I set up and got the photoresistor working for my system to track the light value, and whether that turns out to be high or low. This value is shown on the LCD, within the other values I did in my last milestone. For this to work, I had to try out a couple of different methods to organize and set up the photoresistor, while trying to reduce complications. I used a resistor to make that happen, plus connections along the side of the breadboard and in the analog. In my next and final milestone, I'll program and set up the rain sensor, ESP8266, cooling fan, and programmer adapter. 
  
# Code

```c++
//photoresistor
#define LIGHTPIN A1          
#define LEDPIN 7            
//LightSensor Grove

  int lightValue = analogRead(LIGHTPIN);  

  if (lightValue >= 1000) {  
    digitalWrite(LEDPIN, HIGH);  
  } else {
    digitalWrite(LEDPIN, LOW);  
  }

 lcd.clear();
  lcd.print("Light Sensor");
  lcd.setCursor(0, 1); // Set cursor to the first column (0) and second row (1)
  lcd.print("Light: ");
  lcd.print(lightValue);
  delay(2000);

```
# First Milestone

[![Watch the video](https://img.youtube.com/vi/Nn2hlWvWxzw/0.jpg)](https://youtu.be/Nn2hlWvWxzw?si=3hA88gMOgFd6yoJa)

To complete my first milestone, I developed a system where the LCD would display and decide whether or not the given plant needed water, and automatically start the pump if necessary. To achieve this, I connected the baseboard to the breadboard, which was crucial to the organization, while also providing 5v and GND connections.  Next, I integrated the LCD, soil moisture sensor, and pump into the system. My next step will be setting up the photoresistor to monitor light.

# Schematics 
![image](https://github.com/MakaylaLundry/Makayla_BlueStamp_Portfolio/assets/174461885/e99708e3-fb21-4d33-b445-deb54800ddda)


# Code

```c++
#include <LiquidCrystal.h>


LiquidCrystal lcd(12, 11, 10, 9, 8, 7);
const int AirValue = 693;
const int WaterValue = 290;
const int ThresholdValue = 484;
int soilMoistureValue = 0;
const int RelayPin = 2;


void setup()
{
  Serial.begin(9600);
  lcd.begin(16, 2);
  pinMode(RelayPin, OUTPUT);
  digitalWrite(RelayPin, HIGH);
}


void loop()
{
  soilMoistureValue = analogRead(A0);
  Serial.println(soilMoistureValue);


  lcd.setCursor(0, 0);
  lcd.print("Moisture: ");
  float moisturePercentage = map(soilMoistureValue, AirValue, WaterValue, 0, 100);
  lcd.print(moisturePercentage, 0);
  lcd.print("%");


  int upperLimit = ThresholdValue + 0.1 * (AirValue - WaterValue);
  int lowerLimit = ThresholdValue - 0.1 * (AirValue - WaterValue);


  if (moisturePercentage < 30.0)
  {
    digitalWrite(RelayPin, LOW);
    lcd.setCursor(0, 1);
    lcd.print("Pump: ON ");
  }
  else if (moisturePercentage > 70.0)
  {
    digitalWrite(RelayPin, HIGH);
    lcd.setCursor(0, 1);
    lcd.print("Pump: OFF");
  }
  else
  {
    lcd.setCursor(0, 1);
    lcd.print("Pump: ");
    if (digitalRead(RelayPin) == LOW)
    {
      lcd.print("ON");
    }
    else
    {
      lcd.print("OFF");
    }
  }


  delay(250);
  lcd.clear();
}
```


```c++
// testing/adjesting for air and water value~~

void setup() {
  Serial.begin(9600);
}

void loop() {
  int sensorValue = analogRead(A0);
  Serial.println(sensorValue);
  delay(1000);
}


```

# Bill of Materials

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| 9V Batteries | Powersource | $8.43 | <a href="https://www.amazon.com/dp/B0CGPRL51X/ref=sspa_dk_detail_4?pd_rd_i=B0CGRJVBSD&pd_rd_w=mUq8F&content-id=amzn1.sym.386c274b-4bfe-4421-9052-a1a56db557ab&pf_rd_p=386c274b-4bfe-4421-9052-a1a56db557ab&pf_rd_r=MSRTW7JPG16421NZ30AH&pd_rd_wg=cdpXx&pd_rd_r=0176b04d-f69e-4332-862b-d9063fc2ebe7&s=electronics&sp_csd=d2lkZ2V0TmFtZT1zcF9kZXRhaWxfdGhlbWF0aWM&th=1"> Link </a> |
| 9V Battery Clip | What the item is used for | $5.99 | <a href="https://www.amazon.com/5pack-Battery-2-1mm-Arduino-Corpco/dp/B01AXIEDX8/ref=sr_1_1?crid=1JMB76PI0E2LI&dib=eyJ2IjoiMSJ9.IxZhvVZzjl3mQ3hiFiq1KUOMvd6aWLHUvR5GaRVLvnLpCADw7ptUhm2ZbswcLA3OH-Srpw2qShEwZO-p10V1B08qcOrt0gncPdblQgSH8a_6PHpQ4-_vInA0lzCwWExsJlLpqvGmmsfJvBWkzMQwK15XFLF91dW2yPDl3lBPwRh1puqCFY1goDEn2acNaXvnhlfi_zHFc0AIek0u-9jV-YAmlN9oJPKaoz-6CPWMNs8_wBzmKTDVV8sra3clevWH3BHfH5dBOAWjjR5Fr-MvPr5f6THNw3WOMLeeKYAuS2E.8BHZWnq0i61MogcAFoJqxvFR64QYbjBONOTda2bvQE4&dib_tag=se&keywords=9v+battery+to+barrel&qid=1718991115&s=electronics&sprefix=9v+battery+to+barrel%2Celectronics%2C86&sr=1-1"> Link </a> | 
| 1Digital Multimeter | What the item is used for | $10.99 | <a href="https://www.amazon.com/AstroAI-Digital-Multimeter-Voltage-Tester/dp/B01ISAMUA6/ref=sxin_17_pa_sp_search_thematic_sspa?content-id=amzn1.sym.e8da13fc-7baf-46c3-926a-e7e8f63a520b%3Aamzn1.sym.e8da13fc-7baf-46c3-926a-e7e8f63a520b&cv_ct_cx=digital+multimeter&dib=eyJ2IjoiMSJ9.5LQumrfBR8l0mKnJCJlRg73dxpou0gqYD_ffU3srgs0Utegwth8GcQCSVXVzeZeLSJx5J3itz5TLdmJHsrVITQ.-00jRPoT-bBy26YC4LzQ-S4cYdztgmSMGb83_WEm6HY&dib_tag=se&keywords=digital+multimeter&pd_rd_i=B01ISAMUA6&pd_rd_r=e1ff2570-7e4a-4906-bc55-6f819d48d1bc&pd_rd_w=h7HgL&pd_rd_wg=0ZcFH&pf_rd_p=e8da13fc-7baf-46c3-926a-e7e8f63a520b&pf_rd_r=R6YKX3NXTDQ1PQP4H8RM&qid=1715911879&sbo=RZvfv%2F%2FHxDF%2BO5021pAnSA%3D%3D&sr=1-1-7efdef4d-9875-47e1-927f-8c2c1c47ed49-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9zZWFyY2hfdGhlbWF0aWM&psc=1"> Link </a> |
| L9110S DC Motor Drive Module Stepper | What the item is used for | $7.79 | <a href="https://www.amazon.com/HiLetgo-H-bridge-Stepper-Controller-Arduino/dp/B00M0F243E/ref=sr_1_18?crid=3B9DS11AHPF99&dib=eyJ2IjoiMSJ9.XVQEXNFwGCIYsosoS8koqg3HjESR7duY5uNIxqY7EUaKWzsE_SsLTgcHRRhPwPP22Hy6aQPalQA4VBIcltY0tQvUyFrjC2TaRhvAB53kU5UMg8tz9cm-RRcGiqAR0wIy5-8uGTspJxqiaao5iAe0a2oc0rpE0ypLNZiz8gMOGV5hMacSjU5DAMgMY2ORmp_ImwLl90W8E42yaXY8MHPMYypq1-J6qzIhEZhHSJ6K1qE.V4_l0cjfR8z_468JhztkxyXhUlADt4TVHH44XR90CF0&dib_tag=se&keywords=h+bridge&qid=1718754817&sprefix=h+bridg%2Caps%2C144&sr=8-18"> Link </a> |
| Micro Submersible Mini Water Pump | What the item is used for | $9.99 | <a href="https://www.amazon.com/Sipytoph-Submersible-Flexible-Aquariums-Hydroponics/dp/B097F4576N/ref=sr_1_2?crid=3GFUKHZSUW9UH&dib=eyJ2IjoiMSJ9.f57v5zs0c9bUBDkl7IMgi5J-OOSnvVkGwXoto3NdGdlCEjbJUUjvW9ZEdVK6YXKzS9bNKdmSi2C_g327DzUwUvSv2oRZmD4XsAAz8XLUWexWC0rkceIJudXbfSzO6t8peEF52XbJ_npQ1GJG04edtoNtzO5FGwyuhgpj7dVl_Xmui8a9F7sWlgeO1b1bpPSOokVeyYeEm0uKsENBu-DnaWGwl3R9QrqL8stfg51ZsVeZ34b8mINRZDXV5i67hrtksNmaHuRrpCuBN-s8ex--FNL-Xh7roHXUEF8JV9aajYQ.qnyDT8VLtaXGNz2AKKAfxn6w5qngrgE5GSJu-kAx4E4&dib_tag=se&keywords=arduino+water+pump&qid=1718754653&sprefix=arduino+water+pump%2Caps%2C124&sr=8-2"> Link </a> |
| Arduino UNO R3 Starter Kit | What the item is used for | $49.99 | <a href="https://www.amazon.com/REXQualis-Complete-Development-Detailed-Tutorial/dp/B07BLV5LFY/ref=sr_1_14_sspa?crid=305LJVW81VSYP&dib=eyJ2IjoiMSJ9.y5hO4bhfbA1ueyZdg3qkQkRP6PNtlNLXR7IGb14Ahec2kja4Bj8V9cSRqqEdfp2wnS0wYTfmPHFpGpXj-YJ1iMWZ5lPBMBj5mqQ66znlDc1Jk_D1uN01ZBXJflrdszA_CYSdA-6N6KAYOtOTPq7Gb-lNQ9YdVZm347GtOCkbYdtrVodd52BQfxx7v3MdBFNKJJaif0qcpN6tpvaC226bB-O9ipZ3Ulw-KnOQw3042HGlfgqlTLG4sltHGcEsvuExhTD8hs4wVazGuU6OFHGjAFEaH6WpGhpIfzUxb-iCWBU.MrVna1MXDuAIBJTBh5dSObKppWY7rAPIqpgNIKzJ6mk&dib_tag=se&keywords=arduino+soil+moisture+kit&qid=1718996652&sprefix=arduino+soil+moisture+kit%2Caps%2C78&sr=8-14-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9tdGY&psc=1"> Link </a> |
