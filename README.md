# Macros for Foundry VTT

Foundry VTT (Virtual Tabletop) is a feature-rich, online platform designed for running tabletop role-playing games (RPGs). It offers robust tools for game masters and players, including dynamic lighting, audio integration, and extensive customization options. Foundry VTT supports various game systems, providing a flexible and immersive experience for remote RPG sessions.
<br>
<br>
<div align="center">
<img src="https://i.imgur.com/9LlMPJZ.png" height="80%" width="80%" alt="Failed RDP Steps"/>
</div>
<br>
<p>
Macros in Foundry VTT are highly useful as they automate repetitive tasks, such as rolling dice or managing character abilities, enhancing game efficiency. They streamline gameplay by reducing manual input, allowing game masters and players to focus more on storytelling and strategy. Macros ensure consistency and accuracy in game mechanics, reducing the potential for human error. Additionally, they can be customized to fit specific needs, such as automating complex combat sequences or managing inventory. This flexibility saves time and enhances the gaming experience, making sessions smoother and more enjoyable for everyone involved.
</p>



## Example Usage

I developed and applied a macro to a feature named Cornugon Smash. This macro was integrated with a weapon, ensuring that when the weapon is used, it performs a conditional check to determine if the player has the "Power Attack" ability enabled. Upon confirmation, the macro triggers a dialog box that prompts the player with the option to utilize the Cornugon Smash ability. This enhancement streamlines the decision-making process during gameplay and provides an intuitive user interface for ability management.

<div align="center">
    
![CornugonSmash](https://github.com/user-attachments/assets/b4a91c7d-e738-4034-a15e-7f117e557c4e)

</div>

# Macros
- [Sneak Attack](https://github.com/Steven-Vsqz/Macro-Sneak_Attack)
- 


### Example Code

    // Create the dialog
        new Dialog({
            title: "Cornugon Smash",
            content: content,
            buttons: {
                yes: {
                    label: "Fear My Words!",
                    callback: async () => {
                        // If "Yes" is selected, roll the Intelligence-based skill
                        await actor.rollSkill("int");
                    }
                },
                no: {
                    label: "Sore Throat",
                    callback: () => {
                        // If "No" is selected, do nothing
                        ui.notifications.info("You chose not to attempt to demoralize.");
                    }
                }
            },
            default: "no"
        }).render(true);


