# Womp Womp, Kyle Anthony Vickers
<p align="center">
  <img src="https://imgb.ifunny.co/images/4a5decda433229a1a78b7abefdff53044a1b0f16b70e0c224010f88350bc571c_1.jpg" style="width: 50%;">
</p>

<p align="center" style="font-size: 0.8em; color: #6c757d;"><i>Message to Mr and Mrs. Vickers</i></p>

## Table of Contents

- [Backstory](#backstory)
- [Bad Code](#bad-code)
    - [AI Code](#ai-code)
    - [Stolen Code](#stolen-code)
        - [BLDN (FoxxoSnoot)](#bldn-foxxosnoot)
        - [BloxCity Clone](#bloxcity-clone)
        - [Brick Hill](#brick-hill)
- [Stripe](#stripe)

# Backstory
We gave Kyle tons of warnings in this past year, especially during their startup - when they were using [BloxCity Clone (FoxxoSnoot)](https://github.com/foxxosnoot/bloxcity), he never listened to us, instead downplaying the story severly in the announcements of his server, "Oh yeah a rogue admin hacked our site."; fact check: we aren't an admin. There was an XSS bug (Impossible in 2024), and a bunch more, instead of fixing it he used [ChatGPT](#ai-code).

# Bad Code
Honestly, you aren't ready for this next section, after looking at his code many along with me have found out he's frankensteined 10 source codes together into 1, stolen sources, and straight up used AI Generated Code.

<p align="center">
  <img src="https://i.redd.it/2p4uc6d45yka1.jpg" style="width: 25%;">
</p>

## AI Code
You may ask, "AI is good isn't it, why should I give 2 fucks if Kyle uses ChatGPT, well for one it's insecure AF, as stated by Immersive Labs, ".. could lead to security breaches, including data leaks, unauthorized access, and system failures" - OOPS!

[`BloxCity-Source/app/Models/Item.php`](https://github.com/KyleThePlumber/BloxCity-Source/blob/main/app/Models/Item.php): One instance of AI generated code, as you can tell it's pretty obvious it's AI Generated. 
<img src="https://i.postimg.cc/wvq4BfNx/image.png" style="width:50%; border: 2px solid white;">
<p>For one, the <code>// Assuming the original price is stored in 'cash' column</code>, that's a thing ChatGPT will tell you if you ask it for code, but don't give them all your references.</p>

## Stolen Code

Strap in for this shitshow, turns out kyle has stolen from over 5 or 6 websites to frankenstein it into 1 shit baby site, let's start with FoxxoSnoot's BLDN (Brick Hill Clone)

### BLDN (FoxxoSnoot)
Pretty much the whole Admin Panel including the frontend is actually stolen from BLDN, after kyle public shamed Foxxo for naming his site after Brick Luke.

BloxCity Stolen Code:
<p>
<pre><code>
if ($user->isWearing($item)) {
    // eventually we will forcefully take the item off and re-render the user's avatar
    //$user->takeOffItem($item->id);
    //RenderUser::dispatch($user->id);
}

//if ($item->id == $saintItem && $user->ownsAward(5))
//    $user->removeAward(5);
</code></pre>
</p>

BLDN Code:
<p>
<pre><code>
if ($user->isWearingItem($item->id)) {
    $user->takeOffItem($item->id);
    RenderUser::dispatch($user->id);
}

if ($item->id == $saintItem && $user->ownsAward(5))
  $user->removeAward(5);
</code></pre>
</p>

Bunch more instances, but you get the drift.

### BloxCity Clone

BloxCity Stolen Code:
<p>
<pre><code>
    'item_notifier' => [
        'enabled' => true,
        'webhook' => 'https://discord.com/api/webhooks/1247422520349556757/3z94KZcF0h4n7P2gpXmSvVp-5B1opjc1rlwpMlaCGx_5QHfqZMvgvHkRNz6p1EJx282M',
    ],
    'domains' => [
        'blog' => 'https://blog.bloxcity.com',
        'corp' => 'https://corp.bloxcity.com'
    ],
    'emails' => [
        'support' => 'hello@bloxcity.com',
        'moderation' => 'moderation@bloxcity.com',
        'careers' => 'jobs@bloxcity.com',
        'payments' => 'payments@bloxcity.com'
    ],
    'socials' => [
        'discord' => 'https://discord.gg/6GFAa2faMg',
        'twitter' => 'https://x.com/joinbloxcity',
        'youtube' => 'https://www.youtube.com/u/BLOXCity',
        'instagram' => 'https://www.instagram.com/bloxcity/',
        'threads' => 'https://www.threads.net/@bloxcity',
    ],
</code></pre>
</p>

BloxCity Clone: 
<p>
<pre><code>
    'item_notifier' => [
        'enabled' => false,
        'url' => 'https://discord.com/api/webhooks/812470714401554444/n-lA8LM7rWMq2n7gu4UnEM7d-ZBQoILnpz7zLHygh2Swbko4iBeAvHhdR_MI28ds13Vp'
    ],
    'domains' => [
        'storage' => env('STORAGE_DOMAIN'),
        'blog' => 'https://blog.blox-city.com',
        'corp' => 'https://corp.blox-city.com'
    ],
    'emails' => [
        'support' => 'hello@blox-city.com',
        'moderation' => 'moderation@blox-city.com',
        'careers' => 'hello@blox-city.com',
        'payments' => 'payments@blox-city.com'
    ],
    'socials' => [
        'discord' => 'https://discord.gg/gJ5KNzWxtv',
        'twitter' => 'https://twitter.com/GameBLOXCity',
        'youtube' => '#'
    ],
</code></pre>
</p>

Again, many more instances.

### Brick Hill

BloxCity Stolen Code:
<p>
<pre><code>
    public function __construct()
    {
        $this->mode = 'testing';
        $apiKey = 'DUMBASS LEFT HIS STRIPE KEY';
        $this->client = new StripeClient([
            'api_key' => $apiKey,
            'stripe_version' => '2019-05-16'
        ]);
    }
</code></pre>
</p>

Brick Hill Code: 
<p>
<pre><code>
    public function __construct()
    {
        $this->mode = config('site.payments.mode');
        $apiKey = config("site.payments.stripe.$this->mode.api_key_secret");
        $this->client = new StripeClient([
            'api_key' => $apiKey,
            'stripe_version' => '2020-03-02'
        ]);
    }      
</code></pre>
</p>

They stole the whole page, but want to know what is funny? Even in the Brick Hill source they had the key in a config file, which was using the ENV to hide their secret stripe key, unlike Kyle - pointed out by others in the Anomia Server.

## Stripe
Kyle left his Stripe key in plaintext, not hidden, which exposed this key to the public (Which had all permissions), allowing us to retrieve all costumer data, all addresses etc. We found out that Kyle Anthony Vickers made a grand total of 1,400 USD$ from this site, which we refunded via the Stripe API! Now kyle is in 1.4k USD Debt.

Moral of the story don't play this fucking site.
