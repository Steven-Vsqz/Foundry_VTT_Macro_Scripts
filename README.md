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



## AttackTable

Class for generating multi-attack outputs in a compact format, similar to the pf_attack template in roll20.
Provides highlighting of natural 1s and 20s, and confirmation rolls conditional on the attack roll being a threat.

![CornugonSmash](https://github.com/user-attachments/assets/b4a91c7d-e738-4034-a15e-7f117e557c4e)


### Example Usage

    let attack_bonus = 12;
    let damage = '1d12+9+2d6[sneak attack]';
    let crit = { range: 19, damage: '2d12+18' }; // 19-20/x3 critical
    let table = new AttackTable('Full Attack (Greataxe)');
    await table.addAttack('1st attack', attack_bonus, damage, crit);
    await table.addAttack('2nd attack', attack_bonus - 5, damage, crit);
    table.chat();

Damage rolls are rounded down automatically:

    let table = new AttackTable(`Empowered Scorching Ray`);
    await table.addAttack('1st ray', 10, `(4d6)*1.5`);
    await table.addAttack('2nd ray', 10, `(4d6)*1.5`);
    table.chat();

Combat maneuver checks can use `addManeuver` (damage is optional):

    let cmb = 13;
    let damage = '1d6+4'
    let table = new AttackTable('Grapple');
    await table.addManeuver('', cmb, damage);
    table.chat();

##### With Images and Note:

    let img_bite = '<img src="https://assets.forge-vtt.com/bazaar/systems/pf1/assets/icons/items/inventory/monster-head.jpg" width="20" height="20" style="vertical-align: middle">';
    let img_claw = '<img src="https://assets.forge-vtt.com/bazaar/systems/pf1/assets/icons/items/inventory/monster-paw-bear.jpg" width="20" height="20" style="vertical-align: middle">';
    let table = new AttackTable(`Natural Attacks`);
    await table.addAttack(img_bite + ' Bite', 8, '1d8+4');
    await table.addAttack(img_claw + ' Claw', 8, '1d6+4');
    await table.addAttack(img_claw + ' Claw', 8, '1d6+4');
    table.addNote('Claws also deal 1 bleed on hit.');
    table.chat();

<img src="./img/natural_attacks.png">

##### Healing, Half Damage and Saving Throws:

The function `damageRollAndButton` can be used to add custom damage or healing rolls, for use within notes.

    let table = new AttackTable('Lay on Hands');
    table.addNote('Healing ' + await AttackTable.damageRollAndButton("1d6", {heal: true}));
    table.chat();

<img src="./img/healing.png">

    let table = new AttackTable('Fireball (DC 19)');
    table.addNote('Damage: ' + await AttackTable.damageRollAndButton("10d6", {half: true, save: "ref"}));
    table.chat();

<img src="./img/apply_half.png">

## InputDialog

Class to simplify creation of a dialog that collects user input.

### Example Usage

    let d = new InputDialog('Attack Bonuses', { single: 'Single Attack', full: 'Full Attack' });
    d.addInput('Attack Bonus', 'ab', 2);
    d.addInput('Damage Bonus', 'db', 0);
    d.addCheckbox('Hasted', 'hasted', false);
    d.addSelect('Weapon', 'weapon', ['fists', 'staff']);
    d.render(async (data) => {
        let ab = 5 + data.ab;
        let damage = `1d6+${4 + data.db}`;
        let table = new AttackTable(`Attack (${data.weapon})`);
        await table.addAttack('1st attack', ab, damage);
        if (data.button != 'single') {
            await table.addAttack('Flurry', ab, damage);
            if (data.hasted)
                await table.addAttack('Haste', ab, damage);
        }
        table.chat();
    });
