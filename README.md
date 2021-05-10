# Youtube Bot

Create a way to watch youtube with your friends!

# Installation

```
change the prefix and the token to your
```
# Add FunnyBot 
```
Add FunnyBot and run &yt
```
[FunnyBot](https://discord.com/oauth2/authorize?client_id=787648998403080222&permissions=8&scope=bot)

# Features
- Easy to use
- Useful


# Create your bot

```js
const Discord = require('discord.js');
const client = new Discord.Client();
const fetch = require("node-fetch");

const config = {
    token: "YOUR_TOKEN",
    prefix: "YOUR_PREFIX"}
    
client.on('ready', () => {
    client.user.setActivity(`${config.prefix}youtube`);
    console.log(`${client.user.username} : ${config.prefix} ✅`)
});

client.on('message', message => {
	if(!message.content.startsWith(config.prefix) || message.author.bot) return;
	const args = message.content.slice(config.prefix.length).trim().split(/ +/);
	const command = args.shift().toLowerCase();
	if(command === 'youtube') {
	 const channel =  message.guild.channels.cache.get(args[0]);
            if (!channel || channel.type !== "voice") return message.channel.send(`❌ | Salon spécifié invalide!`);
            if (!channel.permissionsFor(message.guild.me).has("CREATE_INSTANT_INVITE")) return message.channel.send("❌ | J'ai besoin de la permission `CREER UNE INVITATION`");
		 fetch(`https://discord.com/api/v8/channels/${channel.id}/invites`, {
                method: "POST",
                body: JSON.stringify({
                    max_age: 86400,
                    max_uses: 0,
                    target_application_id: "755600276941176913", // youtube together
                    target_type: 2,
                    temporary: false,
                    validate: null
                }),
                headers: {
                    "Authorization": `Bot ${client.token}`,
                    "Content-Type": "application/json"}}).then(res => res.json()).then(invite => {
                    if (invite.error || !invite.code) return message.channel.send(`❌ | Erreur, je ne peux pas commencer l'activité **YouTube**!`);
                    message.channel.send(`✅ | Clique ici pour commencer **YouTube** dans ${channel.name}: <https://discord.gg/${invite.code}>`);
                })
                .catch(e => {
                    message.channel.send(`❌ | Erreur, je ne peux pas commencer l'activité **YouTube**!`);
                    console.log(e)
                })
	} else if(command === 'dev' || command === 'developper') {
		return message.channel.send("From totomate")
	}});
client.login(config.token);
```

# Pictures
![1](/images/1.PNG)

![2](/images/2.PNG)

# Authors
* **[Totomate](https://github.com/Terra-rian/snakecord)** - *Current maintainer*
* **[Snowflake107](https://github.com/Snowflake107)** - *Original idea*

