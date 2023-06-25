# manifold_count_holders
 Counts number of shareholders (traders) of each answer (with > 0 shares) (with YES, NO separately counted) supporting different market types (free response, multiple choice, binary)
 Modify the API key (edit your profile to get one) and the slug name (the short name at the end of the market url) in the config section.

# Examples

## MULTIPLE-CHOICE
```
$ python3 manifold_count_traders.py 
Number of unique traders holding at least one share for each answer in the market (what-is-the-primary-value-users-get):

YES |  NO   -   CHOICE
1   |   0   -   Tool for forecasting
2   |   0   -   Information aggregation
3   |   0   -   Research, analysis, insights
2   |   0   -   Upskilling
5   |   0   -   Speculation (gamification)
```

## BINARY
```
$ python3 manifold_count_traders.py 
Number of unique traders holding at least one share for each answer in the market (1-will-vladimir-putin-be-president):

YES:  788
NO:   398
```

## FREE-RESPONSE
```
$ python3 manifold_count_traders.py 
Number of unique traders holding at least one share for each answer in the market (what-will-the-league-above-diamond):

4  -  Antimatter
2  -  Vibranium
8  -  Mithril
4  -  Origami
3  -  Diamond will be the top league
2  -  Uranium
2  -  Mages
6  -  Clairvoyant
3  -  Unobtainium
3  -  Indigo
2  -  Adamant
20  -  Master
7  -  Emerald
8  -  Crystal
2  -  Platinum
2  -  Paper
11  -  Elite
2  -  Leaderboard
1  -  Diamond 2
19  -  Mythic
2  -  Graphene
1  -  Lonsdaleite
5  -  Roentgenium
7  -  Manifold
5  -  Omega
7  -  It will stay "???"
2  -  Rationalussy
3  -  God
12  -  Oracle
2  -  Infinity
4  -  Metaculus
4  -  Whale
1  -  Bot
1  -  Paper Crane
8  -  The champions league
5  -  Sapphire
3  -  All-Stars
1  -  Time Crystal
3  -  Titanium
1  -  Wolfram
2  -  All-seeing 
3  -  Tungsten
9  -  Champion
1  -  Bose-Einstein condensate
2  -  Plasma
1  -  Photonic Matter
1  -  World League
1  -  Crystal balls
1  -  Nuclear pasta
1  -  Quark-gluon plasma
1  -  Supercritical fluid
3  -  Seers
7  -  Prophet
7  -  Legend
4  -  Prodigy
7  -  Apex
1  -  Magic
6  -  Prescient-ish
1  -  Isaac King
3  -  Super
1  -  Shogath
1  -  AI
1  -  Singularity
1  -  Quintessence
1  -  Schrodinger's League
1  -  Astral
1  -  codex
5  -  Grandmaster
1  -  Wurtzite
1  -  Moissanite
3  -  Computronium
3  -  Aether
1  -  Crystal Ball
1  -  @Mira
1  -  onyx
4  -  The Mythic All-Stars Champions League: Mastering the Prophetic Oracle of the Emerald Crystal Codex - A Singularity of Apex Grandmasters in the Astral Origami Metaculus
2  -  Clairvoyant-ish
3  -  Mantic
1  -  Augur
1  -  Neutronium
1  -  Platonic Idealium
1  -  Silicon
2  -  Mythril
1  -  Hall of fame
1  -  预言家
2  -  Challenger
2  -  Legendary
3  -  Mystic
```
