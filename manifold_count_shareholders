import requests
import time

# Manifold Markets tool for counting number of shareholders by answer
# Counts number of shareholders (traders) of each answer (with > 0 shares) (with YES, NO separately counted) supporting different market types (free response, multiple choice, binary)
# Supports free response, binary, and multiple choice
# Pagination for large numbers of bets is not tested!

####### CONFIG ##########
# Manifold Market API key (get from editing your profile)
api_key = "YOUR-API-KEY-HERE"

# Contract-slug (the short name of the market in the url)
slug = "what-is-the-primary-value-users-get"
#slug = "1-will-vladimir-putin-be-president"
#slug = "what-will-the-league-above-diamond"

#########################

# API request headers
headers = {
    "Authorization": f"Key {api_key}",
}

# URL containing retrieve answer details
answer_url = f"https://manifold.markets/api/v0/slug/{slug}"

# URL containing bet details
bets_url = f"https://manifold.markets/api/v0/bets?contractSlug={slug}"

# API request headers
headers = {
    "Authorization": f"Key {api_key}",
}

# API request to get answer details
def get_answer_details(url):
    response = requests.get(url, headers=headers)
    return response.json()

# API request to get bets
def get_bets(url):
    bets = []
    bets_url = url
    while url:
        response = requests.get(url, headers=headers)
        if response.status_code == 200:
            data = response.json()
            bets += data
            if len(data) == 1000:
                last_id = data[-1]["id"]
                url = f"{bets_url}&before={last_id}"
                time.sleep(10)  # Delay between requests to avoid rate limits
            else:
                url = None
        else:
            print("Error:", response.json()["error"])
            return None
    return bets



# Retrieve answer details
answer_details = get_answer_details(answer_url)
if "error" in answer_details:
    print("Error:", answer_details["error"])
    exit()

market = get_answer_details(answer_url)
if "answers" in market:
    answers = market["answers"]
else:
    # For the binary YES type
    answers = list()
    answers.append({"id" : "YES", "text" : "YES"})
    answers.append({"id" : "NO", "text" : "NO"})    
    
bets = get_bets(bets_url)

# Dictionary to store answer details and filled YES bet count
answer_dict = {}

# Loop through each answer
for answer in answers:
    answer_id = answer["id"]
    answer_text = answer["text"]

    # Count unique traders with filled YES bets for the answer
    filled_yes_bets = set()
    filled_no_bets = set()
    for bet in bets:
        if market["outcomeType"] == "MULTIPLE_CHOICE":
            if bet["answerId"] == answer_id and "isFilled" in bet and bet["isFilled"] and bet["shares"] > 0:
                if bet["outcome"] == "YES":
                    filled_yes_bets.add(bet["userId"])
                elif bet["outcome"] == "NO":
                    filled_no_bets.add(bet["userId"])
        elif market["outcomeType"] == "FREE_RESPONSE":
            if bet["outcome"] == answer_id and bet["shares"] > 0:
                ## make it also work for pools
                filled_yes_bets.add(bet["userId"])
        elif market["outcomeType"] == "BINARY":
            if "isFilled" in bet and bet["isFilled"] and bet["shares"] > 0:
                if bet["outcome"] == "YES":
                    filled_yes_bets.add(bet["userId"])
                elif bet["outcome"] == "NO":
                    filled_no_bets.add(bet["userId"])

    unique_trader_count_yes = len(filled_yes_bets)
    unique_trader_count_no = len(filled_no_bets)
    
    # Add answer details and filled YES bet count to the dictionary
    answer_dict[answer_id] = {
        "answer_text": answer_text,
        "filled_yes_bet_count": unique_trader_count_yes,
        "filled_no_bet_count": unique_trader_count_no
    }    

# Print results
print(f"Number of unique traders holding at least one share for each answer in the market ({slug}):")
print("")
if market["outcomeType"] == "MULTIPLE_CHOICE":
    print ("YES |  NO   -   CHOICE")
    print ("======================")
    for id, data in answer_dict.items():
        answer_text = data["answer_text"]
        print(data["filled_yes_bet_count"], "  |  ", data["filled_no_bet_count"], "  -  ", data["answer_text"])
elif market["outcomeType"] == "BINARY":
    for id, data in answer_dict.items():
        answer_text = data["answer_text"]
        if answer_text == "YES":
            print("YES: ", data["filled_yes_bet_count"])
        elif answer_text == "NO":
            print("NO:  ", data["filled_no_bet_count"])
elif market["outcomeType"] == "FREE_RESPONSE":
    for id, data in answer_dict.items():
        print(data["filled_yes_bet_count"], " - ", data["answer_text"])
