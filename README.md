# Ammo UI

### In this tutorial, we will be making an ammo UI, in which each bullet is physically displayed on screen, and disappears when you fire. We will also be programming a reload mechanic.

> [!IMPORTANT]
> You will need any version of Unity and VisualStudio released within the last 5 years
> 
> This tutorial is made for a 3D Project
> 
> For this tutorial, you will need to download a .png of the bullets you wish to use, and have an empty .png of the same size. Ensure that it has no background for best results. 

> [!NOTE]
> This tutorial shares the same project as my other tutorial, **Camera Waypoints** and **Crosshair Cursor**. Due to how specific this tutorial is, it is recommended you check out the first two.

### To avoid any confusion, let's take a quick look at the Heirarchy;

<img width="168" alt="image" src="https://github.com/user-attachments/assets/225e31c9-98ca-417a-b8a0-ddddf88004ae" />

> **A** is an empty GameObject that houses the Camera (**B**) and a Canvas parented to the Crosshair UI (**C**). Anything to do with the Player and UI will be in here.


### We'll start by creating the Ammo UI

1. Right click your existing `Canvas` -> `UI` -> `Canvas`. Hit F2 to rename as 'Bullet UI'.

2. Change `Render Mode` to 'Screen Space - Camera' and drag your `Main Camera` to the `Render Camera` tab.

![image](https://github.com/user-attachments/assets/79900c2a-8aa2-4d85-a5d6-04056d6b47ed)

3. Right click `Bullet UI` -> `UI` -> `Image`, rename as 'Bullet'.

4. Drag and drop your bullet and empty png's to the `assets` window. For both png's you'll need to change the `Texture Type` from 'Default' to 'Sprite (2D and UI). Scroll down and click `Apply`.

![image](https://github.com/user-attachments/assets/d8047131-c4bb-4773-bf1a-ac8404208b61)

> You'll know it's worked because there's a play icon on the images.

5. Click your Bullet GameObject in `Heirarchy` and drag your bullet image to `Source Image`. Click the `Set Native Size` button below. You can check the position and size of your image by clicking on `Game` in the top left. Scale and position it however you like. To create more, click on `Bullet` and press Ctrl + D to duplicate.

<img width="960" alt="image" src="https://github.com/user-attachments/assets/28ceda51-e87a-4878-9457-b9d5dfc6bb9d" />


### Next we'll make the UI Script

1. Right Click in the `Assets` window, -> `Create` -> `C# Script` and name the script 'AmmoDisplay'. Double click to open in VisualStudio.

2. We need to add the UI library, so Hit `Enter` on **Line 3** and type in `using UnityEngine.UI;`.

3. Under `public class`, insert the following:

   `public int ammo;`
   `public int maxAmmo;`
   > public means you can edit the numbers from Unity

   `public Sprite emptyRound;`
   `public Sprite fullRound;`
   > this allows you to drag and drop sprites within Unity

   `public Image[] bullets;`
   > [] is an array, which allows you to drag and drop multiple gameObjects within Unity

> [!NOTE]
> GameObject must be an **IMAGE** and not a **RAW IMAGE**

![image](https://github.com/user-attachments/assets/643c8a44-e41b-4dda-966d-e29930e6ddcb)

4. Save with Ctrl + S and return to Unity. Right click `Bullet UI` -> `Create Empty Parent`, F2 and rename 'Gun'.

5. Drag and drop your AmmoDisplay script onto `Gun`. It should look something like this:

![image](https://github.com/user-attachments/assets/1cf9cc59-85d1-4ec5-bd0c-8d8904b7c344)

6. Set Ammo and Max Ammo to the number of bullets you have displayed on your UI. Then, drag and drop your bullet sprite to `Full Round` and the empty png to `Empty Round`.

7. If you click the arrow besides `Bullets` under the `Ammo Dispaly (Script)`, you'll see a box that says the List is empty. You can mass import your Images by clicking the lock icon in the top right of the `Inspector`, shift click your bullets in `Heirarchy` and drag them to the indicated space.

<img width="431" alt="image" src="https://github.com/user-attachments/assets/10c6dc73-38a9-4185-8cd7-c0064ff7ea8f" />

![image](https://github.com/user-attachments/assets/22138793-329e-4143-bab1-c2ae874e1520)
> This ensures the order remains the same


### Now we need to add the shooting part of the script

1. Return to AmmoDisplay in VisualStudio. Under the array, let's add a bool--which is a true or false statement. Type `public bool isFiring;`

2. Under `void Update()`, type in the following:

   `if (Input.GetMouseButtonDown(0) && !isFiring && ammo > 0)
   {
        isFiring = true;
        ammo--;
        isFiring = false;
   }`

> `Input.GetMouseButtonDown(0)` is Left Mouse Button (you can assign any button you want really). `&&` seems to imply all of the requirements need to be met for the if statement to work. The last three lines are to ensure you only lose 1 ammo per click, rather than continuously.

3. The next part of the script will ensure that the full and empty bullet sprites are shown accordingly. Type in:

   `for (int i = 0; i < bullets.Length; i++)
   {
        if (i < ammo)
        {
            bullets[i].sprite = fullRound;
        }
        else
        {
            bullets[i].sprite = emptyRound;
        }`
> If ammo is above 0, it displays a bullet, otherwise it displays an empty round.

 `      if (i < maxAmmo)
        {
            bullets[i].enabled = true;
        }
        else
        {
            bullets[i].enabled = false;
        }`
> (I think) This determines which bullets in the array are displayed, based on your ammo count.

4. Save your script and return to Unity.


### If you run your project with the script showing in the `Inspector`, you'll see that the ammo count goes down when you click (or press the allocated button). However, there's no way to replenish bullets...
### Let's create a Reload script

1. Right Click in the `Assets` window, -> `Create` -> `C# Script` and name the script 'Reload'. Double click to open in VisualStudio.

2. Hit `Enter` on **Line 3** and type in `using UnityEditor;`.

3. We're going to add a line under `public class` that allows this script to communicate with the AmmoDisplay script.

   `public AmmoDisplay ammoDisplay;`

4. Below this, we're going to create a void, which is a return function (no, I don't know what that means).

   `void reloadAmmo
   {
       int maxAmmo = 6;
       ammoDisplay.ammo = maxAmmo;
   }`
   > Where I've put 6, you will put your max ammo number.

5. Under `void Update()`, we're going to assign the reload function to a button. I'm going to assign it to space bar, but you can insert whichever key you want.

   `if (Input.GetKey("space"))
        {
            reloadAmmo();
            return;
        }`

![image](https://github.com/user-attachments/assets/3f91c729-f77d-41ad-bdee-e4884e58d43c)

6. Save your script and return to Unity.
  
7. Drag and drop your Reload script onto `Gun`. Set `Ammo Display` to `Gun (Ammo Display)` and save.


### Run your game and now you should be able to reload.
