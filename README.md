import os,requests,uuid,threading

from time import sleep as slp

from colorama import Fore,Style

from user_agent import generate_user_agent as gua

# FREE Tool By @O0Dev (Telegram channel)

# To Buy a stronger & more updated version contact me on telegram => @o_7ay

# All rights reserved for @O0Dev (Telegram channel) 2021 | Coder : Osama A.M.Y 

class O0Dev():

    def __init__(self):

        self.link = requests.get('https://o7aa.pythonanywhere.com/?id=7238',headers={'user_agent':gua()}).json()['telegram']

        self.wait = 0

        self.uuid = uuid.uuid4()

        self.b0 = Style.RESET_ALL

        self.b1 = Fore.YELLOW + '['

        self.b2 = Fore.YELLOW + ']'

        self.b3 = Fore.GREEN + '-'

        self.b4 = Fore.RED + '!'

        self.b5 = Fore.LIGHTCYAN_EX + '+'

        self.bb = (Fore.LIGHTYELLOW_EX+f"""

                                                

_____ ___ ____             _____               

|     |   |    \ ___ _ _   |   __|_ _ _ ___ ___ 

|  |  | | |  |  | -_| | |  |__   | | | | .'| . |

|_____|___|____/|___|\_/   |_____|_____|__,|  _|

                                        |_|  

    [-] Coded By Osama A.M.Y || Tele {self.link}

    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

        """)

        self.headers = {

                'User-Agent': 'Instagram 113.0.0.39.122 Android (24/5.0; 515dpi; 1440x2416; huawei/google; Nexus 6P; angler; angler; en_US)',

                "Accept": "*/*",

                "Accept-Encoding": "gzip, deflate",

                "Accept-Language": "en-US",

                "X-IG-Capabilities": "3brTvw==",

                "X-IG-Connection-Type": "WIFI",

                "Content-Type": "application/x-www-form-urlencoded; charset=UTF-8",

                'Host': 'i.instagram.com',

                'Connection': 'keep-alive'

            }

        

    def Exit(self):

        os.system('cls' if os.name == 'nt' else 'clear')

        print(self.bb)

        slp(1)

        exit(input(f'{self.b1}{self.b5}{self.b2}{self.b0} Press Enter to close : '))

    def igLogin(self):

        os.system('cls' if os.name == 'nt' else 'clear')

        print(self.bb)

        username = input(f'{self.b1}{self.b5}{self.b2}{self.b0} ur Username : ')

        password = input(f'{self.b1}{self.b5}{self.b2}{self.b0} ur Password : ')

        

        if username and password:

            url = 'https://i.instagram.com/api/v1/accounts/login/'

            data = {

                'uuid': self.uuid,

                'password': password,

                'username': username,

                'device_id': self.uuid,

                'from_reg': 'false',

                '_csrftoken': 'missing',

                'login_attempt_countn': '0'

            }

            login = requests.post(url, headers=self.headers, data=data)

            loginJson = login.json()

            self.loginCookies = login.cookies

            loginre = login.text

            if 'Please check your username and try again.' in loginre:

                print(f'{self.b1}{self.b4}{self.b2}{self.b0} please check username and try again')

                self.Exit()

            else:

                if 'logged_in_user' in loginre:

                    print(f'{self.b1}{self.b3}{self.b2}{self.b0} Successfully login')

                    slp(2)

                    os.system('cls' if os.name == 'nt' else 'clear')

                    print(self.bb)

                    self.userInformation()

                else:

                    if 'The password you entered is incorrect' in loginre:

                        print(f'{self.b1}{self.b4}{self.b2}{self.b0} information false try again')

                        self.Exit()

                    else:

                        if 'Please wait a few minutes before you try again.' in loginre:

                            print(f'{self.b1}{self.b4}{self.b2}{self.b0} You cant login , your Ip is blocked from instagram')

                            self.Exit()

                        else:

                            if 'challenge_required' in loginre:

                                MyPATH = loginJson['challenge']['api_path']

                                url_api = 'https://i.instagram.com/api/v1' + MyPATH

                                Secure = requests.get(url_api, headers=self.headers, cookies=self.loginCookies).json()

                                mode = []

                                if ('email') in Secure['step_data']:

                                    mode.append('[1] Email')

                                elif ('phone_number') in Secure['step_data']:

                                    mode.append('[0] Phone')

                                else:

                                    print(f'{self.b1}{self.b4}{self.b2}{self.b0} Error! Try Again later')

                                    self.Exit()

                                for modes in mode:

                                    print(modes)

                                myMode = input(f"{self.b1}{self.b5}{self.b2}{self.b0} Enter your Mode : ")

                                SecureData = {

                                    'choice': myMode,

                                    '_uuid': self.uuid,

                                    '_uid': self.uuid,

                                    '_csrftoken': 'missing'

                                }

                                Send_Mode = requests.post(url_api, headers=self.headers, data=SecureData, cookies=self.loginCookies).json()

                                Contact = Send_Mode['step_data']['contact_point']

                                print(f'{self.b1}{self.b3}{self.b2}{self.b0} Done Sending The Code To » {Contact}')

                                myCode = input(f'{self.b1}{self.b5}{self.b2}{self.b0} Enter Your Code : ')

                                CodeData = {

                                    'security_code': myCode,

                                    '_uuid': self.uuid,

                                    '_uid': self.uuid,

                                    '_csrftoken': 'missing'

                                }

                                Send_Code = requests.post(url_api, headers=self.headers, data=CodeData, cookies=self.loginCookies).text

                                if 'logged_in_user' in Send_Code:

                                    print(f'{self.b1}{self.b3}{self.b2}{self.b0} Successfully login')

                                    slp(2)

                                    os.system('cls' if os.name == 'nt' else 'clear')

                                    print(self.bb)

                                    self.userInformation()

                                else:

                                    print(f'{self.b1}{self.b4}{self.b2}{self.b0} Error Code !')

                                    self.Exit()

                            else:

                                self.Exit()

        else:

            self.igLogin()

    def userInformation(self):

        account_information = 'https://i.instagram.com/api/v1/accounts/current_user/?edit=true'

        gett = requests.get(account_information, headers=self.headers,cookies=self.loginCookies).json()

        try:

            self.email = gett['user']['email']

            self.setTarget()

        except:

            print(f'{self.b1}{self.b4}{self.b2}{self.b0} link email in your account and try again')

            self.Exit()

    def setTarget(self):

        self.target = input(f'{self.b1}{self.b5}{self.b2}{self.b0} User Target : ')

        self.thread = int(input(f'{self.b1}{self.b5}{self.b2}{self.b0} Enter Thread [25] : '))

        readyOrNot  = input(f'{self.b1}{self.b5}{self.b2}{self.b0} Ready To Swap Now [y/n] : ')

        if readyOrNot == 'y' or readyOrNot == 'Y':

            if self.target and self.thread:

                self.speedSwap()

            else:

                self.igLogin()

        else:

            self.Exit()

        

    # To Buy a stronger & more updated version contact me on telegram => @o_7ay

    def swapO0Dev(self):

        sessionid = self.loginCookies['sessionid']

        changeUrl = 'https://www.instagram.com/accounts/edit/?__a=1' # in full version Connection is api and fast

        headers = {

            'accept': '*/*',

            'accept-encoding': 'gzip, deflate, br',

            'accept-language': 'en-US,en;q=0.9',

            'content-length': '121',

            'content-type': 'application/x-www-form-urlencoded',

            'cookie': f'mid=YcXr6gALAAEpgAyz0KYFGcL0wMos; ig_did=D25D9D16-AA20-4C3E-B183-C57E9B68F0FC; ig_nrcb=1; csrftoken=k32fHTbEPPC0k2gAN66XJw2fJN8U1uj1; ds_user_id=49055251094; sessionid={sessionid}; shbid="11096\05449055251094\0541671896961:01f733cebf6e08cc9e2a7c76f716e1e9c45267ee8c55ea1546741d7d6b8ac2aae282864f"; shbts="1640360961\05449055251094\0541671896961:01f7c6f7793787621659a4e8f2715cc2dffb45d858eba2456e1d1553dea60c44eba6045d"; rur="RVA\05449055251094\0541671896997:01f74dd7ba61bdcfafc6eecf8cfcc016983f72d8da9293af510ec0db86df07147cdc4823"',

            'origin': 'https://www.instagram.com',

            'referer': 'https://www.instagram.com/accounts/edit/',

            'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36 Edg/96.0.1054.62',

            'x-csrftoken': 'k32fHTbEPPC0k2gAN66XJw2fJN8U1uj1',

            'x-ig-app-id': '936619743392459',

            'x-ig-www-claim': 'hmac.AR3zUSSxBZYU_BeKFbgMtpGrtgLFSMtTMDdTGLIMUMgLqL3c',

            'x-instagram-ajax': '05272981ffad',

            'x-requested-with': 'XMLHttpRequest'

        }

        chData = {

            'first_name': '',

			'email': self.email,

			'username': self.target,

			'phone_number': '',

			'biography': 'Swapped Done By @o.7a',

			'external_url': 't.me/O0Dev',

			'chaining_enabled': 'on'

        }

        while True:

            Swap = requests.post(changeUrl,headers=headers,data=chData)

            if Swap.status_code == 200:

                print(f'{self.b1}{self.b3}{self.b2}{self.b0} Successfully Swap : @{self.target}\n{self.b1}{self.b3}{self.b2}{self.b0} Coded by Osama A.M.Y')

                self.Exit()

            elif Swap.status_code == 400:

                print(f'{self.b1}{self.b4}{self.b2}{self.b0} The transfer has not been completed !!')

            elif Swap.status_code == 429:

                print(f'{self.b1}{self.b4}{self.b2}{self.b0} The account is blocked')

                self.Exit()

    def speedSwap(self):

        thredas = []

        for i in range(self.thread):

            t = threading.Thread(target=self.swapO0Dev)

            t.daemon = True

            thredas.append(t)

            t.start()

        else:

            for i in thredas:

                i.join()

O0Dev().igLogin()

# FREE Tool By @O0Dev (Telegram channel)

# All rights reserved for @O0Dev (Telegram channel) 2021 | Coder : Osama A.M.Y 
