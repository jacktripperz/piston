# Piston Intro

The "Piston", is a deflationary daily ROI platform that allows
you to earn up to 1% daily return on your investment sustainably through a tax system
on transactions. It also allows team building Pit Crews through a referral system. 

## Disclaimer
Signing transactions via this script requires the use of a **`wallet's private key`** meaning you need to **`handle your private key locally`** on the computer from which you want to run this script on.
By using this script **`you agrees to take full responsibility`** for your private key and wallets security!
**`I take no responsibility`** in lost funds, wallets or anything related to using this script.
The script relies on many things - such as blockchain congestion, dropped network packages, etc. I have tried to implement some resilience to the script but even though it runs by itself, **`you have the responsibility`** to watch it, maintain it and make sure it doesn't run wild or unexpectingly.

## Prerequisites
1. A clean and secure computer/nuc/raspberry pi that can run 24/7.
2. Minor programming knowledge

## The Piston project

The [Piston](https://piston-token.com/ref/jacktz) is a low risk, high reward contract that operates similar to a high yield 
certificate of deposit. You can participate by purchasing the token through these steps: 
1. Go to [Piston](https://piston-token.com/ref/jacktz) and deposit piston into your Pit Crew.

In order to get the most out of your staked funds is to compound and claim with a strategy - for instance, compound 6 days in a row and claim 1, and then repeat.
The purpose of this code is to do this automatically for you. 

## Setup

This code was specifically written to be as secure as possible, since signing transactions requires the use of
a wallet's private key. It's imparative you use the encryption outlined in the code to best protect yourself
in the event your computer is ever compomised. 

1. Download [Python](https://www.python.org/downloads/) if you do not already have it. I was not able to get this code
to work on Python 3.9, so I would recommending using Python 3.7 or 3.8. There are a number of resources that will walk 
you through installing Python depending on your operating system.

2. Once Python is installed, the following packages need to be installed.

web3, cryptography, python-dotenv
 ```bash
$ python -m pip install web3
$ python -m pip install cryptography
$ python -m pip install python-dotenv
```

3. In a python terminal, import `cryptography` and encrypt your private key
```py
>>>from cryptography.fernet import Fernet
>>>key = Fernet.generate_key()
>>>key.decode()
```

4. Open `.env.example` and replace the key with the output from `key.decode()`. Copy in without plingers. Save the file without '.example' at the end. Make sure the file type is saved as 'ENV'. 

5. Go back to the python terminal and do the following:
```py
>>>fernet = Fernet(key)
>>>encMessage = fernet.encrypt('YOURPRIVATEKEYHERE'.encode())
>>>encMessage.decode()
```

6. Take the output value from the last line `encMessage.decode()`, create a file called `key.txt` and save the output in the file. 
7. Save the `key.txt` to the root of the project.

8. Create a file called `pa.txt`, paste your public wallet address in and save the file to the root of the project.
9. Copy the file `cycle_config.example.json` and save it as `cycle_config.json`. This file contains the definition of your strategy cycle.  [See the Cycle settings](#cycle-settings) on how to modify your cycle strategy.

## Cycle settings
The script includes a cycle-manager. This means that you can determine a cycle on when to `roll` (compound/nitro) and when to `claim`.
The file called `cycle_config.example.json` shows an example on how a cycle could look like.
One cycle includes 4 inputs:
- Id (1-indexed, meaning that the first cycle should always start with 1)
- Type (either use `roll` or `claim`)
- EndTimerAt (Specifies the time of day where the cycle ends. For example with "20:00" (8pm) or "08:00" (8am). You can set the time of day as you please. By adding two or more cycles, you can setup your strategy to run every 3rd day, 12h or all the way down to each minute)
- MinimumPiston (you might be able to `roll` because 24h has past but you only want to `roll`, when you have a minimum Piston of this value)

Each cycle is defined by one iteration. Set as many iterations you want - just make sure to increment the `Id` of each iteration. When the cycle ends, it starts again from the top.

Defaults for each iteration in the example is set to `roll` and to execute every day at "20:00" (8pm).

### Persisted cycle settings
Cycle settings from your `cycle_config.json` are persisted. This means that the `nextCycleId` property is updated at the end of every cycle and you cycle loop never changes, so if you ever have to restart the script your cycle will never lose state and it will start from where it left off.

## Usage

In a terminal window, navigate to the location where you saved all the files. Run the `race.py` file.

```bash
$ python race.py
```

This terminal window will always need to remain open for the script to function. If the terminal window closes, just execute
`python race.py` again.

# Donations
If this script helps you, consider supporting me by sending an airdrop: 
- **wallet:** *0x361472B5784e83fBF779b015f75ea0722741f304*

Or using my referral code:
- [Piston](https://piston-token.com/ref/jacktz)


# Other projects to take a look at:
- [DRIP Faucet](https://drip.community/faucet?buddy=0x361472B5784e83fBF779b015f75ea0722741f304) - 1% per day - low risk, high reward, no decay! Get the [auto-script here](https://github.com/jacktripperz/hydrator)
- [Animal Farm, PiggyBank](https://theanimal.farm/piggybank/0x361472B5784e83fBF779b015f75ea0722741f304) - 3% per day - high risk, high reward! Get the [auto-script here](https://github.com/jacktripperz/piggybanker)
- [Animal Farm, Garden](https://theanimal.farm/referrals/0x361472B5784e83fBF779b015f75ea0722741f304) - 3% per day, high risk, high reward! Get the [auto-script here](https://github.com/jacktripperz/planter)
- [Baked Beans](https://bakedbeans.io?ref=0x361472B5784e83fBF779b015f75ea0722741f304) - 8% per day, high risk, high reward! Get the [auto-script here](https://github.com/jacktripperz/bakedbeans)
- [BNB Miner](https://bnbminer.finance?ref=0x361472B5784e83fBF779b015f75ea0722741f304) - 3% per day, high risk, high reward! Get the [auto-script here](https://github.com/jacktripperz/bnbminer)
- [My DiamondTeam v2](https://mydiamondteam.online/v2/?ref=0x361472b5784e83fbf779b015f75ea0722741f304) - 1.5% per day - low risk, high reward, no decay, 5% reinvest bonus! Get the [auto-script here](https://github.com/jacktripperz/diamond_team)
