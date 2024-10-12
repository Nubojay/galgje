import random



def woordkeuze():
    global random_woord
    try:
        f = open("woordenlijst.txt", "r")
    except:
        print('er was een fout met het openen van de woorden lijst, de file word gesloten')
        f.close
    woorden = f.readlines()
    random_woord = random.choice(woorden)
    random_woord = random_woord.strip()
    f.close

    return random_woord


#TODO INPUT VAN GOK MAX 1 LETTER MAKEN


def galgje():
    woordkeuze()
    naam = input('vul hier je naam in: ')
    print('Welkom', naam, '!')
    global gewonnen
    gewonnen = False
    fout = ''
    goed = ''
    klaar = False
    poging = 11
    leeg = len(random_woord)  * '_ '
    geraden = leeg.split(' ')
    del geraden[-1]
    print(geraden)

    while klaar == False:
        print('je mag nog', poging, 'keer raden.')
        gok = input('\ngok hier een letter:')
        gok = gok.lower()
        if len(gok) > 1 :
            print('je kan maar 1 letter raden')
        elif gok in '1234567890':
                print('Je kan geen cijfers raden')
        else:
            for letter in gok:
                if letter in goed or letter in fout:
                    print('deze letter is al geraden! Raad een andere letter.')
                if letter in random_woord and letter not in goed:
                    print('Goed geraden!')
                    goed = goed + letter + ' '
                elif letter not in random_woord and letter not in fout:
                    fout = fout + letter + ' '
                    print('Helaas probeer een andere letter')
                    poging -= 1

            for i in range(len(random_woord)):
                if random_woord[i] == gok:
                    geraden[i] = gok


            print('je goed geraden letters zijn : \n' + goed, '\n' 'en je fout geraden letters zijn : \n' + fout,  '\n' , geraden )

        if poging == 0:
            print('het goede woord was:', random_woord)
            klaar = True
            opnieuw_spelen()
        if '_' not in geraden:
            klaar = True
            gewonnen = True
            print('GEFELICITEERD JE HEBT GEWONNEN')
            opnieuw_spelen()




def opnieuw_spelen():
    jalst = ['Ja', 'ja', 'yes', 'Yes']
    opnieuw = input('Wil je opnieuw spelen? ja/nee : ')
    if opnieuw in jalst :
        global random_woord
        random_woord = woordkeuze()
        galgje()
    else:
        print('Goodbye :)')





#Deze woorden lijst is gegenereerd door CHATGPT
