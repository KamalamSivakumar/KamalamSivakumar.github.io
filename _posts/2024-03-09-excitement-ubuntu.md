## ubuntu, git and overthinking

I procrastinated for more than 3 months to install ubuntu in dual boot setting. I thought that it was a cumbersome and tricky task.
Turns out I only need a 12gb/12gb+ pen drive, an etcher software and I'm good to go. The whole process took only about an hour. The procedure is as follows. 

1. Download Ubuntu software. (https://ubuntu.com/download/desktop)

2. Install an etcher software, I used balenaetcher. (https://etcher.balena.io/)

3. Open the etcher and etch the downloaded Ubuntu file. 

4. Go to boot options by pressing F2/F10/F12 continously while restarting.

5. In the prompt, choose your hardrive.

6. Follow the instructions carefully, in the part were creating partitions, there'll be an option that says "partition along with Windows Boot Manager", choose that and adjust space as needed.

7. Follow along, and you're done!

PS: Along with installing, you also get the prompt to try Ubuntu!

That was it. I was so elated. Thank you thozha, for all your help. 
Ubuntu brings back so many memories of my lab classes during college. The excitement to learn new things. Those days were lovely. These days are too.

The next thing I wish I did during my college days was profiling my git.
Kamalam you should have! It's so important to have your git placed, as a portfolio of your works. Now I'm building one, in my own space and pace, just like this blog. 

The next thing I was elated about was learning how to use git from Ubuntu terminal using ssh. 
It felt so so good. 
It's simple. 
The steps.

1. Create an ssh keypair from the website. (https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

2. 2 files would be generated sshkey and sshkey.pub

3. Link the sshkey to your github account. (settings->ssh and gpg keys->add key->paste your sshkey.pub file's content)

4. Make sure the ssh agent is running from your terminal, and check if you have linked it to github by typing the command: "ssh -T git@github.com". If you get something that starts with "Hi!.." then pakka, else you'll have to revisit and check.

5. Now you can clone repos to your desktop.

The next was how to push changes onto git from desktop. Basic I learnt is as follows.

1. git add "your work name" (Adding the modified/new work to git's list)

2. git commit-m "meaningful message" (Asking git to notify about this change we're about to do with a tagline)

3. git push -u -f origin main (force pushing our work from theh ssh upstream onto the specified remote repository's main branch) 

That's it! I'm yet to try out git merge, pull and pushing onto other branches than main.
Will update this post then!

Learning something new can be initimidating and exciting at the same time, but it's ulti ulti cool! Makes me feel like I'm in THE ZONE, which I am.
I'm going to push myself to learn more!

This song always makes me feel in the zone. Check it out!
[![Pistah daa]](https://www.youtube.com/watch?v=SuuypjzzqRw)

Taata!

