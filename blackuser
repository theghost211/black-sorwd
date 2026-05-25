#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
╔══════════════════════════════════════════════════════╗
║           ULTIMATE USERNAME HUNTER X               ║
║           Platinum Edition – v4.2 (ALL PLATFORMS)   ║
║           Licensed to: ghost.com1                   ║
╚══════════════════════════════════════════════════════╝
"""

import os
import sys
import time
import random
import string
import platform
import json
import re
import requests
from colorama import Fore, Style, init

init(autoreset=True)

# ═══════════════════════════════════════════
#  إعدادات الترخيص
# ═══════════════════════════════════════════
LICENSE_KEY = "ghost.com1"
MAX_ATTEMPTS = 3

# ═══════════════════════════════════════════
#  قواعد المنصات
# ═══════════════════════════════════════════
SOCIAL_MEDIA = {
    "Instagram": "https://www.instagram.com/{}/",
    "TikTok": "https://www.tiktok.com/@{}",
    "Snapchat": "https://www.snapchat.com/add/{}",
    "Facebook": "https://www.facebook.com/{}",
    "Telegram": "https://t.me/{}",
    "GitHub": "https://github.com/{}",
    "Reddit": "https://www.reddit.com/user/{}",
    "Pinterest": "https://www.pinterest.com/{}/",
    "Twitch": "https://www.twitch.tv/{}",
    "Kick": "https://kick.com/{}",
    "Threads": "https://www.threads.net/@{}",
    "Tumblr": "https://{}.tumblr.com",
    "Steam": "https://steamcommunity.com/id/{}",
}

GAMING = {
    "Roblox": "https://www.roblox.com/users/profile?username={}",
    "Minecraft": "https://namemc.com/search?q={}",
    "EpicGames": "https://store.epicgames.com/u/{}",
    "Steam": "https://steamcommunity.com/id/{}",
    "Xbox": "https://xboxgamertag.com/search/{}",
    "PlayStation": "https://psnprofiles.com/{}",
    "Valorant": "https://tracker.gg/valorant/profile/riot/{}/overview",
    "Fortnite": "https://fortnitetracker.com/profile/all/{}",
    "PUBG": "https://pubg.op.gg/user/{}",
    "LeagueOfLegends": "https://www.op.gg/summoners/na/{}",
}

EMAIL_DOMAINS = [
    "gmail.com", "outlook.com", "hotmail.com",
    "yahoo.com", "icloud.com", "proton.me"
]

# ═══════════════════════════════════════════
#  أدوات مساعدة وتأثيرات بصرية
# ═══════════════════════════════════════════
def slow_print(text: str, delay: float = 0.02, color: str = Fore.WHITE):
    for char in text:
        sys.stdout.write(color + char)
        sys.stdout.flush()
        time.sleep(delay)
    print()

def draw_spinner(duration: float, message: str = "Loading"):
    spinner = ["|", "/", "-", "\\"]
    end_time = time.time() + duration
    while time.time() < end_time:
        for frame in spinner:
            sys.stdout.write(f"\r{Fore.LIGHTCYAN_EX}[{frame}] {message}...")
            sys.stdout.flush()
            time.sleep(0.1)
    sys.stdout.write("\r" + " " * 40 + "\r")

def elegant_clear():
    for _ in range(3):
        print("\n" * 5)
        time.sleep(0.03)
    os.system("cls" if platform.system() == "Windows" else "clear")

def validate_username(username: str) -> bool:
    return bool(re.match(r'^[a-zA-Z0-9._-]{1,30}$', username))

# ═══════════════════════════════════════════
#  نظام الترخيص
# ═══════════════════════════════════════════
def check_license():
    elegant_clear()
    print(Fore.LIGHTCYAN_EX + "╔══════════════════════════════════════════════╗")
    print(Fore.LIGHTCYAN_EX + "║                                              ║")
    slow_print("║       🔐 LICENSE ACTIVATION REQUIRED 🔐      ║", 0.03, Fore.LIGHTYELLOW_EX)
    print(Fore.LIGHTCYAN_EX + "║                                              ║")
    slow_print("║     Enter your key to unlock the legend      ║", 0.03, Fore.WHITE)
    print(Fore.LIGHTCYAN_EX + "║                                              ║")
    print(Fore.LIGHTCYAN_EX + "╚══════════════════════════════════════════════╝")
    
    for attempt in range(1, MAX_ATTEMPTS + 1):
        key = input(f"\n{Fore.LIGHTYELLOW_EX}[?] License Key ({attempt}/{MAX_ATTEMPTS}): {Fore.WHITE}").strip()
        
        if key == LICENSE_KEY:
            print(f"\n{Fore.LIGHTGREEN_EX}[✓] Validating license", end="")
            draw_spinner(1.5, "Decrypting")
            print(f"\n{Fore.LIGHTGREEN_EX}[✓] LICENSE ACTIVATED SUCCESSFULLY!")
            slow_print("Welcome, Legend! The hunt begins now...", 0.04, Fore.LIGHTCYAN_EX)
            time.sleep(1)
            elegant_clear()
            return True
        
        print(f"{Fore.LIGHTRED_EX}[✗] Invalid key!")
        if attempt < MAX_ATTEMPTS:
            print(f"{Fore.LIGHTYELLOW_EX}[!] {MAX_ATTEMPTS - attempt} attempts left.\n")
    
    print(f"\n{Fore.LIGHTRED_EX}╔══════════════════════════════════════════════╗")
    print(f"{Fore.LIGHTRED_EX}║   [✗] LICENSE VERIFICATION FAILED         ║")
    print(f"{Fore.LIGHTRED_EX}║   [✗] Exiting with style...               ║")
    print(f"{Fore.LIGHTRED_EX}╚══════════════════════════════════════════════╝")
    time.sleep(2)
    sys.exit(1)

# ═══════════════════════════════════════════
#  مدير جلسات HTTP
# ═══════════════════════════════════════════
class SessionManager:
    def __init__(self):
        self.session = requests.Session()
        self.session.headers.update({
            "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
        })
    
    def get(self, url: str, **kwargs) -> requests.Response:
        return self.session.get(url, timeout=kwargs.pop("timeout", 10), **kwargs)
    
    def close(self):
        self.session.close()

# ═══════════════════════════════════════════
#  دوال الفحص (جميعها مطبقة بدقة)
# ═══════════════════════════════════════════
class PlatformCheckers:
    def __init__(self, session: SessionManager):
        self.session = session
        self.checkers = {
            "Instagram": self.check_instagram,
            "TikTok": self.check_tiktok,
            "Snapchat": self.check_snapchat,
            "Facebook": self.check_facebook,
            "GitHub": self.check_github,
            "Reddit": self.check_reddit,
            "Twitch": self.check_twitch,
            "Kick": self.check_kick,
            "Threads": self.check_threads,
            "Tumblr": self.check_tumblr,
            "Steam": self.check_steam,
            "Roblox": self.check_roblox,          # المصححة
            "EpicGames": self.check_epicgames,
            "PlayStation": self.check_psnprofiles,
            "Valorant": self.check_valorant,
            "Fortnite": self.check_fortnite,
            "PUBG": self.check_pubg,
            "LeagueOfLegends": self.check_leagueoflegends,
            "Minecraft": self.check_minecraft,
            "Xbox": self.check_xbox,
        }
    
    def get_checker(self, platform: str):
        return self.checkers.get(platform, self.generic_check)
    
    def check_instagram(self, username, url_template):
        url = url_template.format(username)
        try:
            r = self.session.get(url, timeout=8)
            if r.status_code == 404:
                return "AVAILABLE"
            match = re.search(r'window\.__INITIAL_STATE__\s*=\s*({.*?});', r.text)
            if not match:
                match = re.search(r'window\._sharedData\s*=\s*({.*?});', r.text)
            if match:
                data = json.loads(match.group(1))
                user = data.get("user") or data.get("entry_data", {}).get("ProfilePage", [{}])[0].get("graphql", {}).get("user")
                if user is None:
                    return "AVAILABLE"
                return "TAKEN"
            if "Sorry, this page isn't available." in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_tiktok(self, username, url_template):
        oembed_url = f"https://www.tiktok.com/oembed?url=https://www.tiktok.com/@{username}"
        try:
            r = self.session.get(oembed_url, timeout=10)
            if r.status_code == 200 and "author_name" in r.json():
                return "TAKEN"
            if r.status_code == 404:
                return "AVAILABLE"
        except:
            pass
        url = url_template.format(username)
        try:
            r = self.session.get(url, timeout=10)
            if r.status_code == 404:
                return "AVAILABLE"
            if "Couldn't find this account" in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_snapchat(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            if r.status_code == 404 or "Sorry, we couldn't find that page" in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_facebook(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8, allow_redirects=True)
            if r.status_code == 404 or "This content isn't available right now" in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_github(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            return "AVAILABLE" if r.status_code == 404 else "TAKEN"
        except:
            return "ERROR"
    
    def check_reddit(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            if r.status_code == 404 or "Sorry, nobody on Reddit goes by that name." in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_twitch(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            if r.status_code == 404 or "This channel does not exist" in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_kick(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            if r.status_code == 404 or "Sorry, this page isn't available" in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_threads(self, username, url_template):
        return self.check_instagram(username, url_template)
    
    def check_tumblr(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            if r.status_code == 404 or "There's nothing here." in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_steam(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            if r.status_code == 404 or "The specified profile could not be found." in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"

    # -------------------------------------------
    #  فحص Roblox المُصحَّح (يقرأ JSON بدقة)
    # -------------------------------------------
    def check_roblox(self, username, url_template):
        """
        يستخدم API الرسمي:
        GET https://users.roblox.com/v1/users/get-by-username?username={username}
        يفحص JSON: إذا وُجد errors -> AVAILABLE، إذا وُجد Id -> TAKEN
        """
        api_url = f"https://users.roblox.com/v1/users/get-by-username?username={username}"
        try:
            r = self.session.get(api_url, timeout=10)
            if r.status_code == 200:
                data = r.json()
                if "errors" in data:
                    return "AVAILABLE"
                if data.get("Id") is not None:
                    return "TAKEN"
                return "AVAILABLE"
            elif r.status_code in (404, 400):
                return "AVAILABLE"
            else:
                return self._roblox_fallback(username, url_template)
        except:
            return self._roblox_fallback(username, url_template)

    def _roblox_fallback(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            if r.status_code == 404:
                return "AVAILABLE"
            if "Incorrect username" in r.text or "Page cannot be found" in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_epicgames(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            if r.status_code == 404 or "Page Not Found" in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_psnprofiles(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            if r.status_code == 404 or "The requested player could not be found" in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_valorant(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            if r.status_code == 404 or "Player not found" in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_fortnite(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            if r.status_code == 404 or "Player not found" in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_pubg(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            if r.status_code == 404 or "No user found" in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_leagueoflegends(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            if r.status_code == 404 or "Summoner not found" in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_minecraft(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            if r.status_code == 404 or "No results found" in r.text:
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def check_xbox(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8)
            if r.status_code == 404 or "not found" in r.text.lower():
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"
    
    def generic_check(self, username, url_template):
        try:
            r = self.session.get(url_template.format(username), timeout=8, allow_redirects=True)
            if r.status_code == 404:
                return "AVAILABLE"
            final_url = r.url.rstrip('/')
            if url_template.format(username).split('/')[2] not in final_url:
                return "AVAILABLE"
            if "not found" in r.text.lower() or "doesn't exist" in r.text.lower():
                return "AVAILABLE"
            return "TAKEN"
        except:
            return "ERROR"

# ═══════════════════════════════════════════
#  الكلاس الرئيسي – بتصميم بصري فاخر
# ═══════════════════════════════════════════
class UsernameHunterX:
    def __init__(self):
        self.session_manager = SessionManager()
        self.checker = PlatformCheckers(self.session_manager)
        self.running = True
    
    def show_banner(self):
        elegant_clear()
        print(Fore.LIGHTMAGENTA_EX + """
    ██╗   ██╗███████╗███████╗██████╗
    ██║   ██║██╔════╝██╔════╝██╔══██╗
    ██║   ██║███████╗█████╗  ██████╔╝
    ██║   ██║╚════██║██╔══╝  ██╔══██╗
    ╚██████╔╝███████║███████╗██║  ██║
     ╚═════╝ ╚══════╝╚══════╝╚═╝  ╚═╝
    """ + Fore.LIGHTGREEN_EX + """
    ██╗  ██╗██╗   ██╗███╗   ██╗████████╗███████╗██████╗
    ██║  ██║██║   ██║████╗  ██║╚══██╔══╝██╔════╝██╔══██╗
    ███████║██║   ██║██╔██╗ ██║   ██║   █████╗  ██████╔╝
    ██╔══██║██║   ██║██║╚██╗██║   ██║   ██╔══╝  ██╔══██╗
    ██║  ██║╚██████╔╝██║ ╚████║   ██║   ███████╗██║  ██║
    ╚═╝  ╚═╝ ╚═════╝ ╚═╝  ╚═══╝   ╚═╝   ╚══════╝╚═╝  ╚═╝
    """)
        print(Fore.LIGHTCYAN_EX + "╔══════════════════════════════════════════════╗")
        print(Fore.LIGHTCYAN_EX + "║                                              ║")
        print(Fore.LIGHTCYAN_EX + "║   " + Fore.LIGHTGREEN_EX + "[1] SOCIAL MEDIA" + Fore.LIGHTCYAN_EX + "                        ║")
        print(Fore.LIGHTCYAN_EX + "║   " + Fore.LIGHTCYAN_EX + "[2] GAMING" + Fore.LIGHTCYAN_EX + "                             ║")
        print(Fore.LIGHTCYAN_EX + "║   " + Fore.LIGHTYELLOW_EX + "[3] EMAIL GENERATOR" + Fore.LIGHTCYAN_EX + "                    ║")
        print(Fore.LIGHTCYAN_EX + "║   " + Fore.LIGHTRED_EX + "[4] EXIT" + Fore.LIGHTCYAN_EX + "                                ║")
        print(Fore.LIGHTCYAN_EX + "║                                              ║")
        print(Fore.LIGHTCYAN_EX + "╚══════════════════════════════════════════════╝")
        print(Fore.WHITE + "\n   Licensed to: " + Fore.LIGHTYELLOW_EX + "ghost.com1")
        print(Fore.WHITE + "━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━")
    
    def generate_username(self, length):
        return ''.join(random.choices(string.ascii_lowercase + string.digits, k=length))
    
    def show_platform_list(self, platforms):
        print()
        for i, name in enumerate(platforms.keys(), 1):
            print(Fore.LIGHTGREEN_EX + f"   [{i}] {name}")
        print(Fore.LIGHTRED_EX + "   [0] Back to Main Menu")
        print()
    
    def select_output_method(self):
        print(Fore.LIGHTGREEN_EX + "\n   [1] Terminal")
        print(Fore.LIGHTCYAN_EX + "   [2] Discord Webhook")
        print(Fore.LIGHTYELLOW_EX + "   [3] Telegram Bot")
        method = input(Fore.WHITE + "\n   Select > ")
        webhook = token = chat_id = None
        if method == "2":
            webhook = input("   Webhook URL: ")
        elif method == "3":
            token = input("   Bot Token: ")
            chat_id = input("   Chat ID: ")
        return method, webhook, token, chat_id
    
    def send_result(self, method, result, webhook, token, chat_id):
        if method == "1":
            print(result)
        elif method == "2" and webhook:
            try:
                requests.post(webhook, json={"content": result})
            except:
                pass
        elif method == "3" and token and chat_id:
            try:
                requests.post(f"https://api.telegram.org/bot{token}/sendMessage",
                             data={"chat_id": chat_id, "text": result})
            except:
                pass
    
    def scan_platform(self, platform_name, url_template, username_length,
                     method, webhook, token, chat_id):
        elegant_clear()
        print(Fore.LIGHTMAGENTA_EX + f"\n[+] Hunting on {platform_name}...")
        print(Fore.LIGHTYELLOW_EX + "[!] Press CTRL+C to stop\n")
        checker_func = self.checker.get_checker(platform_name)
        try:
            while self.running:
                username = self.generate_username(username_length)
                if not validate_username(username):
                    continue
                status = checker_func(username, url_template)
                if status == "AVAILABLE":
                    result = Fore.LIGHTGREEN_EX + f"[AVAILABLE] {username}"
                elif status == "TAKEN":
                    result = Fore.LIGHTRED_EX + f"[TAKEN] {username}"
                else:
                    result = Fore.LIGHTYELLOW_EX + f"[ERROR] {username}"
                self.send_result(method, result, webhook, token, chat_id)
                time.sleep(0.5)
        except KeyboardInterrupt:
            print(Fore.LIGHTRED_EX + "\n[!] Hunt Stopped")
            time.sleep(1)
    
    def email_generator(self):
        while True:
            elegant_clear()
            print(Fore.LIGHTCYAN_EX + "╔══════════════════════════════════════════════╗")
            print(Fore.LIGHTCYAN_EX + "║          EMAIL GENERATOR                    ║")
            print(Fore.LIGHTCYAN_EX + "╚══════════════════════════════════════════════╝")
            print(Fore.LIGHTRED_EX + "\n[Type 'back' to return to main menu]\n")
            length_input = input(Fore.LIGHTYELLOW_EX + "Username Length > ").strip().lower()
            if length_input == 'back':
                return
            if not length_input.isdigit():
                print(Fore.LIGHTRED_EX + "Invalid input! Enter a number or 'back'.")
                time.sleep(1)
                continue
            length = int(length_input)
            while True:
                username = self.generate_username(length)
                print(Fore.LIGHTCYAN_EX + "\nGenerated Email Ideas:\n")
                for domain in EMAIL_DOMAINS:
                    print(Fore.LIGHTGREEN_EX + f"   {username}@{domain}")
                again = input(Fore.LIGHTYELLOW_EX + "\nGenerate again? (y/n/back): ").lower()
                if again == 'back':
                    return
                if again != 'y':
                    break
    
    def social_media_section(self):
        while True:
            elegant_clear()
            print(Fore.LIGHTMAGENTA_EX + "╔══════════════════════════════════════════════╗")
            print(Fore.LIGHTMAGENTA_EX + "║         " + Fore.LIGHTCYAN_EX + "SOCIAL MEDIA PLATFORMS" + Fore.LIGHTMAGENTA_EX + "              ║")
            print(Fore.LIGHTMAGENTA_EX + "╚══════════════════════════════════════════════╝")
            self.show_platform_list(SOCIAL_MEDIA)
            choice = input(Fore.WHITE + "Select Platform > ").strip()
            if choice == '0':
                return
            if not choice.isdigit() or int(choice) < 1 or int(choice) > len(SOCIAL_MEDIA):
                print(Fore.LIGHTRED_EX + "Invalid choice!")
                time.sleep(1)
                continue
            choice = int(choice) - 1
            names = list(SOCIAL_MEDIA.keys())
            platform_name = names[choice]
            platform_url = SOCIAL_MEDIA[platform_name]
            length = int(input("Username Length > "))
            method, webhook, token, chat_id = self.select_output_method()
            self.scan_platform(platform_name, platform_url, length, method, webhook, token, chat_id)
    
    def gaming_section(self):
        while True:
            elegant_clear()
            print(Fore.LIGHTMAGENTA_EX + "╔══════════════════════════════════════════════╗")
            print(Fore.LIGHTMAGENTA_EX + "║            " + Fore.LIGHTCYAN_EX + "GAMING PLATFORMS" + Fore.LIGHTMAGENTA_EX + "                 ║")
            print(Fore.LIGHTMAGENTA_EX + "╚══════════════════════════════════════════════╝")
            self.show_platform_list(GAMING)
            choice = input(Fore.WHITE + "Select Platform > ").strip()
            if choice == '0':
                return
            if not choice.isdigit() or int(choice) < 1 or int(choice) > len(GAMING):
                print(Fore.LIGHTRED_EX + "Invalid choice!")
                time.sleep(1)
                continue
            choice = int(choice) - 1
            names = list(GAMING.keys())
            platform_name = names[choice]
            platform_url = GAMING[platform_name]
            length = int(input("Username Length > "))
            method, webhook, token, chat_id = self.select_output_method()
            self.scan_platform(platform_name, platform_url, length, method, webhook, token, chat_id)
    
    def main_menu(self):
        while True:
            self.show_banner()
            section = input(Fore.WHITE + "\n   Choose Section > ").strip()
            if section == "1":
                self.social_media_section()
            elif section == "2":
                self.gaming_section()
            elif section == "3":
                self.email_generator()
            elif section == "4":
                elegant_clear()
                slow_print("See you next time, hunter!", 0.04, Fore.LIGHTRED_EX)
                self.session_manager.close()
                sys.exit(0)
            else:
                print(Fore.LIGHTRED_EX + "Invalid choice!")
                time.sleep(1)

# ═══════════════════════════════════════════
#  نقطة البداية
# ═══════════════════════════════════════════
if __name__ == "__main__":
    if check_license():
        app = UsernameHunterX()
        try:
            app.main_menu()
        except KeyboardInterrupt:
            elegant_clear()
            slow_print("See you next time, hunter!", 0.04, Fore.LIGHTRED_EX)
        finally:
            app.session_manager.close()
