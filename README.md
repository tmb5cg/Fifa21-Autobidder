# TMB's FIFA 21 Autobidder


## Intro

Note - Originally built for me and my friends as a fun side project, I'm making it open source because it deserves street credit. This is my first experience with tkinter (for GUI) as well as Selenium WebDriver, which is a library that can interact with any site.

An Autobidder is a form of bot deployed on the Transfer Market in FIFA Ultimate Team's web application.

Unlike the more common and widely known (look up link to story about bots) botting methods such as an Autobuyers (link to Chithak's) or player snipers (link to discord 'filters'), which rely on a combination of speed and luck (such as that one snipe that makes your week), Autobidding as a botting method relies on lower margins at higher volumes - without any luck involved. This makes Autobidding not only more lucrative long term, but also more consistent, safer and secure in comparison.

The preferred botting method used by coin farmers working on industrial scales (yes this is a thing - trust me), it is one of the lesser known botting methods employed by FIFA nerds for a variety of reasons. The main reason being its complexity (but also maybe because it is less fun, you're not running the chance of sniping Gullit for 20k coins)

In terms of complexity, a simple Autobuyer can be built in as simple as a '''for''' loop clicking search, checking for a result, and trying again. An Autobidder requires managing multiple bidding wars in real time.

Used effectively, once your competitors are scared away after trying to tire out a computer, the market is cornered and auctions will be won for significantly under market value. While everyone else is trying to snipe Ronaldo for 5k, and all of them competing with each other for the same snipe, small but consistent gains at scale will prevail (we're living in a simulation).

Compared to an autobuyer, auto bidding excels in terms of:
- Consistency
- - Does not rely on luck, more importantly not competing with other bots (think of how many bots just searched for Ronaldo as you read this)
- Efficiency
- - Guaranteed profits since supply of undervalued auctions is infinitely greater than snipes
- Security / Detectability
- - Selenium's Javascript injection is the only indication of something 'off' - thankfully Selenium in itself is harmless, and no different than an Adblocker's injected Javascript
- Complexity
- - This was a lot of work so I hope someone finds this useful

It is for these reasons I sought to create the ultimate Autobidder entirely on my own to maximize profits while also flying as low profile as possible.


## How it works

Built in Python, this bot uses Selenium to interact with FUT Webapp via Chromedriver (insert link) and features a tkinter(insert link) User Interface for easy operation.

Unlike other bots, its operations can be monitored in real time, and appears identical to a human's actions. It is also safer than other Javascript injection bots, as the only Javascript injected is Selenium's, rendering EA's bot detection useless. Chromedriver flags have also been obfuscated, although the scale of EA's bot detection seems tiny so this is done out of an abundance of caution.

Features:
- Autobid on up to 5 players simultaneously
- Dynamic GUI displays logs and stats in real time from autobidder and autobuyer methods.
- All methods are threaded separately, so GUI is always active
- Optional AutoLogin + authentication code entry (requires enabling 3rd party access in Gmail)


[insert gif of autobidding]

Initial bids will reap low profit, but once you fight off other bidders, you have the player cornered. You will start winning players for 350 that you can sell for 800. These margins at high volumes reap ~30k coins an hour.


Project Structure
-Main.py is gui tkinter, creates selenium driver
-on button click, calls thread runner which creates autobidder. driver is passed along
- autobidder creates helper

![](./readme/windows_gui.png)


Mac Login:

![](https://user-images.githubusercontent.com/58413404/109426177-37160500-79ba-11eb-94b5-f04f570f6b47.mp4)


The first step is logging in, either manually or automatically.

Once logged in, click the Start Autobidder button.

On the initial pass through the market, Futbin's price will be used as ceiling. During this time, all market data will be logged, and upon initial run's completion, parsed to determine the accurate market price. The Actual Market price will be used from then on.

## Installation

First, download a fresh version of Chromedriver straight from Google here (insert link) as it must match your machine's version of Chrome. Replace the existing chromedriver that matches your platform in either the chrome_linux, chrome_mac, or chrome_windows folders.

Navigate to the project's root directory via Terminal or Command Prompt, in this example it is on my Desktop.

Terminal: 

'''
cd ~/Desktop/FIFA21UTBOTv2
'''

Command Prompt:
'''
cd Desktop\FIFA21UTBOTv2
'''

Then run the following to install Selenium and any other requirements (see requirements.txt): 

```
pip install -r requirements.txt
```

Make sure pip is installed (see here). If there are any errors, such as 'missing xyz module', simply ''' pip install [xyz] '''. Feel free to post an issue on this Repository and I'd be happy to trouble shoot. 

For any other errors, see *troubleshooting*. 

## Troubleshooting

subsection: python

    Python3 or greater is required to run the program. The most likely cause for errors is having an outdated Python version installed. To see your version of Python:

    Mac
    Open Terminal and type
    '''
    python --version
    '''

    Windows
    Open Command Prompt and type
    '''
    insert cmd
    '''

    If you see Python 2.x, see *here* for installing Python 3. 

    If you know you have Python 3 installed, but see 2.x, your system's Python PATH must be assigned to Python 3.x. To do this, see here for Mac and here for Windows [insert link to sent to Ben]. 

    I suspect this will cause the biggest number of issues.

subsection: chromedriver

    If the bot is correctly starting, and you are sure Python is not the issue, then Chromedriver is the issue. The Chromedriver files (folder chrome_windows / chrome_mac) are the versions used by my system. In order for Chromedriver to work, it must match your systems version of Chrome. This can easily be fixed by redownloading Chromedriver.

    Go *here* and download the relevant chromedriver file. Replace the chromedriver in either the chrome_windows or chrome_mac with your download. 


Windows


## Configuration

Everything is configured via the user interface. 

To add a player, retrieve their Futbin (insert link) URL and click Add Player. The bot will automatically open the Futbin link and retrieve the data, which will populate in the table.

The maximum bid ceiling is hard set to 85%, and will be customizeable in a later update. The sell price is 95% of market price. 


### Automatic login

If you would like to automatically login, enable Auto Login via the UI.

A '''logins.txt''' file will be created in the data folder, which must be structured like this:

'''
1st line: Webapp email
2nd line: Webapp password
3rd line: Access code email
4th line: Access code password
'''

Email credentials are necessary to fetch the authorization code.

**Remember to enable third party app access in Gmail, see here:** 

```
EMAIL_CREDENTIALS = {
    "email": "your_email@example.com",
    "password": "your_password",
}
```

## Running

**Linux/Mac systems**

In Terminal, run:

```
make run
```

See [troubleshooting] for help. 

**Windows**

Set the PYTHONPATH variable with the value of the code directory - [check this link](https://stackoverflow.com/questions/3701646/how-to-add-to-the-pythonpath-in-windows-so-it-finds-my-modules-packages).

Run:

```
python src\main.py
```


## Info

I encourage you to reach out with any errors, and would love contributors.

Good luck!


# To do
- update refresh page and go to watchlist method to not be on a timer
- make playerlist better interactable
- make player list not baked in stone upon starting autobidder
