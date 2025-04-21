from translate import Translator
import urllib.request
from bs4 import BeautifulSoup
import sys
import time
import threading

def loading_dots(stop_event):
    """Displays loading dots until the stop_event is set."""
    while not stop_event.is_set():
        for dot_count in range(1, 4):
            if stop_event.is_set():
                break
            sys.stdout.write("\rLoading" + "." * dot_count + "   ")  # Add spaces to clear extra dots
            sys.stdout.flush()
            time.sleep(0.5)
    sys.stdout.write("\rDone!          \n") 

def Transl(input_text):
    greek_lang=Translator(to_lang="el")

    try:
        out_text= greek_lang.translate(input_text)
        stop_event.set()
        loading_thread.join()
        return out_text
    except:
        print("An error occured when translating")

stop_event = threading.Event()
loading_thread = threading.Thread(target=loading_dots, args=(stop_event,))
loading_thread.start()
#read from meeting the book
try:
    with urllib.request.urlopen('https://wol.jw.org/en/wol/meetings/r1/lp-e/2025/4') as f:
        meatingtext= f.read().decode('utf-8')
except:
    print("An error occured when opening meeting webpage")
idworld="(30 min.) <a href=\"" 
try:
    index=meatingtext.index(idworld)
    index=index+len(idworld)  
except:
    print("Error occured when finding index")
bookurl=""
while (meatingtext[index]!='\"'):
    bookurl+=meatingtext[index]
    index+=1

#read from book to verses
try:
    with urllib.request.urlopen(f'https://wol.jw.org{bookurl}') as f:
        booktext= f.read().decode('utf-8')
        
except:
    print("An error occured when opening book webpage")


idworld="class=\"themeScrp\"><strong>Based on</strong> <a href=\"" 
try:
    index=booktext.index(idworld)
    index=index+len(idworld)  
except:
    print("Error occured when finding index")
bibleurl=""
while (booktext[index]!='\"'):
    bibleurl+=booktext[index]
    index+=1


#read from Bible
try:
    with urllib.request.urlopen(f'https://wol.jw.org{bibleurl}') as f:
        bibletext= f.read().decode('utf-8')
        
except:
    print("An error occured when opening bible webpage")
soup= BeautifulSoup(bibletext,'html.parser')
divs_tag=soup.find_all('div',class_='studyNoteGroup')
for div in divs_tag:
    if div:
        h3_tag=div.find_previous('h3')
        p_tag=div.find('p')
        ptext=p_tag.text
        chunks=[]
        if len(ptext)>500:
            pwords=ptext.split()
            
            current_chunk = ""
            for word in pwords:
                if len(current_chunk)+len(word)+1> 500:
                    chunks.append(current_chunk)
                    current_chunk=word
                else:
                    current_chunk +=(" "if current_chunk else "")+word
            if  current_chunk:
                    chunks.append(current_chunk)

        else:
            chunks.append(ptext)

        
        #Translation Part
        verse=Transl(h3_tag.text)
        print(verse,end=' ')
        for ch in chunks:
            commends=Transl(ch)
            print(commends ,end=' ')
        print("\n")



