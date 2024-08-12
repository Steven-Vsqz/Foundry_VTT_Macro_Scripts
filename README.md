# Foundry VTT

Foundry VTT (Virtual Tabletop) is a feature-rich, online platform designed for running tabletop role-playing games (RPGs). It offers robust tools for game masters and players, including dynamic lighting, audio integration, and extensive customization options. Foundry VTT supports various game systems, providing a flexible and immersive experience for remote RPG sessions.
<br>
<br>
<div align="center">
<img src="https://i.imgur.com/9LlMPJZ.png" height="80%" width="80%" alt="Failed RDP Steps"/>
  <h3>🛠️Languages & Tools Used!</h3>

  ![image](https://img.shields.io/badge/JavaScript-323330?style=for-the-badge&logo=javascript&logoColor=F7DF1E)
  ![image](https://img.shields.io/badge/ChatGPT-74aa9c?style=for-the-badge&logo=openai&logoColor=white)
</div>

<!-- TOC -->
## Table of Contents
- [What are Macros?](#macros-in-a-nutshell)
- [Instructions](#instructions)
- [List of Macros]()
  - [Cornugon Smash](#cornugon-smash)
  - [Healing Spell & Potion Tracker](#healing-spell-and-potion-tracker)
  - [Sneak Attack](#sneak-attack)
  - [Targeted Token Info](#targeted-token-info)
 
<!-- /TOC -->

## Macros in a nutshell
<p>
Macros in Foundry VTT are highly useful as they automate repetitive tasks, such as rolling dice or managing character abilities, enhancing game efficiency. They streamline gameplay by reducing manual input, allowing game masters and players to focus more on storytelling and strategy. Macros ensure consistency and accuracy in game mechanics, reducing the potential for human error. Additionally, they can be customized to fit specific needs, such as automating complex combat sequences or managing inventory. This flexibility saves time and enhances the gaming experience, making sessions smoother and more enjoyable for everyone involved.
</p>

<details close>
<summary>

  ## Instructions
      
</summary>
    
- Choose the weapon/item/feature you want the script to execute on.
- Open the weapon/item/feature panel by Right clicking.
- Navigate to the "Advanced" tab.
  
<img src="https://i.imgur.com/lrkobCc.png" height="40%" width="50%" alt="SneakAttack"/>

- In the "Script Calls" section, click the "+" button to add a new script.
- Paste the provided code into the new script section.
- Give the script a name of your choice.
<img src="https://i.imgur.com/AxUcD3r.png" height="40%" width="50%" alt="SneakAttack"/>

- Done!

</details>

<details close>
  <summary>

  ## Cornugon Smash 
    
  </summary>
  <h2>Description</h2>
  When "Power Attack" is active, this script triggers a dialog box asking if you want to use "Cornugon Smash" to intimidate your target. The dialog is well-styled and even shows off your Intimidation modifier in   green, making it easy to see your potential impact.
  
  ```lua
    // Check if isPowerAttack is true
    if (isPowerAttack === true) {
        (async () => {
  ```
  
  You can choose to proceed with the demoralize attempt or skip it entirely. The script ensures a token is selected before doing anything and gives a heads-up, if no token is selected.
  

  <img src="https://i.imgur.com/lybQDsa.png" height="40%" width="50%" alt="SneakAttack"/>
  <hr>
</details>




<details close>
<summary>
   
## Healing Spell and Potion Tracker

</summary>
  <h2>Description</h2>
  This script helps you manage your healing spells and potions/extracts in Foundry VTT. It shows a dialog box where you can pick a spell from a list (like Cure Light Wounds), and it tells you how many prepared charges are left. 
  <br />
  <br />
  
  If you choose a spell, it automatically subtracts one charge and updates your character sheet.
  ```lua
  // Subtract 1 charge
      preparedAmount -= 1;
  
  // Update the spell with the new preparedAmount
      await spell.update({ "data.preparation.preparedAmount": preparedAmount });
  ```
  It also checks your inventory for any potions or extracts that start with "Potion of Cure" or "Extract of Cure" and shows you how many you have left.
  
  ```lua
  // Search for potions and extracts in the inventory
      const inventoryItems = actor.items.filter(item => item.name.startsWith("Potion of Cure") || item.name.startsWith("Extract of Cure"));
      let itemQuantities = {};
      inventoryItems.forEach(item => {
      itemQuantities[item.name] = item.data.data.quantity || 0;
      });
  ```
  A simply and clean interface. It provides you with the information you need without having to manually view your resources.
  
  ![Healing bomb](https://github.com/user-attachments/assets/246c3966-9316-4f65-bbfa-3c8c9ecfef51)
  <hr>   
 
 </details>

<details close>
<summary>
  
## Sneak Attack
</summary>
  <h2>Description</h2>
  When you want to apply sneak attack damage in your game, this macro gets your rogue's level, figures out how many dice you should roll, and pops up a dialog box. You can choose to roll the damage with a bit of stylish flavor text or skip it for now. It’s a fun way to   add some flair to your sneak attacks!
  <br />
  <br />
  
  Calculates how many sneak attack dice you get based on your rogue level. Doesn't have to be only rogues, any class that grants you sneak attack can be placed here. Just change the `actor.classes.(class)` to the one you want.
  ```lua
  // Calculate the number of sneak attack dice
    let rogueLevel = actor.classes.rogue?.level || 0;
    let numDice = Math.ceil(rogueLevel / 2);
  ```
  ![Sneak Attack](https://github.com/user-attachments/assets/82e4eabb-8c8c-40c6-8d4a-c2ab19b7eaa5)

  Just to add some stylish flavor text to the attack, the script randomly picks from a list of pre-made phrases to display. 
  ```lua
  // Function to get a random flavor
    function getRandomFlavor() {
      return flavors[Math.floor(Math.random() * flavors.length)];
    }
  ```

  <h3>Displayed result:</h3>
  <img src="https://i.imgur.com/KLHUM0S.png" height="40%" width="40%" alt="SneakAttack"/>
  <hr>   
</details>

<details close>
  <summary>
    
  ## Targeted Token Info
    
  </summary>
  <h2>Description</h2>
  <p>When you target a token on the canvas, this script gathers all sorts of information about that character, including their name, hit points, ability scores, armor class, combat stats, and even what buffs     they're under. It also lists their weapons, equipment, and other features like class abilities, feats, and spells. All of this is presented in a clean, easy-to-read dialog box with sections that you can expand   or collapse as needed. The layout includes some helpful tooltips to explain what each stat means, and it uses some slick styling to make the info pop. If you forget to target a token, the script will remind you with an error notification.</p>
    
  ![Token Info](https://github.com/user-attachments/assets/94e24b24-355d-41dd-8e14-50e45199f6a4)
<hr>
</details>
