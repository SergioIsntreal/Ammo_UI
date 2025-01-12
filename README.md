# Ammo UI

### In this tutorial, we will be making an ammo UI, in which each bullet is physically displayed on screen, and disappears when you fire. We will also be programming a reload mechanic.

> [!IMPORTANT]
> In this tutorial, you will need any version of Unity and VisualStudio released within the last 5 years
> 
> This tutorial is made for a 3D Project
> 
> For this tutorial, you will need to download a .png of the bullets you wish to use, and have an empty .png of the same size. Ensure that it has no background for best results. 

> [!NOTE]
> This tutorial shares the same project as my other tutorial, **Camera Waypoints** and **Crosshair Cursor**. Due to how specific this tutorial is, it is recommended you check out the first two.

### To avoid any confusion, let's take a quick look at the Heirarchy;

<img width="168" alt="image" src="https://github.com/user-attachments/assets/225e31c9-98ca-417a-b8a0-ddddf88004ae" />

> **A** is an empty GameObject that houses the Camera (**B**) and a Canvas housing the Crosshair UI (**C**). Anything to do with the Player and UI will be in here.


### We'll start by creating the Ammo UI

1. Right click your existing `Canvas` -> `UI` -> `Canvas`. Hit F2 to rename as 'Bullet UI'.

2. Change `Render Mode` to 'Screen Space - Camera' and drag your `Main Camera` to the `Render Camera` tab.

![image](https://github.com/user-attachments/assets/79900c2a-8aa2-4d85-a5d6-04056d6b47ed)

3. Right click `Bullet UI` -> `UI` -> `Image`, rename as 'Bullet'.

4. Drag and drop your bullet and empty png's to the `assets` window. For both png's and change the `Texture Type` from 'Default' to 'Sprite (2D and UI). Scroll down and click `Apply`.

![image](https://github.com/user-attachments/assets/d8047131-c4bb-4773-bf1a-ac8404208b61)

> You'll know it's worked because there's a play icon on the images.

5. Click your Bullet GameObject in `Heirarchy` and drag your bullet image to `Source Image`. Click the `Set Native Size` button below. You can check the position and size of your image by clicking on `Game` in the top left. Scale and position it however you like. To create more, click on `Bullet` and press Ctrl + D to duplicate.

![image](https://github.com/user-attachments/assets/fc0f6c5b-41c9-4390-b9c1-1ee332ec5249)


### Now let's make the display script


