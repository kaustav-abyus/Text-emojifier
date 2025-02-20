cmd commands:
pip install emoji

python code:

import emoji
#taking user input
user_input=input("Enter your sentence")
#filtering puntuations and numbers from sentence
filtered_sentence=""
for i in user_input:
    if(i in "qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM" or i==" "):
        filtered_sentence=filtered_sentence+i
filtered_sentence=filtered_sentence.lower()
seperated_words=filtered_sentence.split(" ")    


#creating a list of all avaiilable emojis in library
emoji_list= list(emoji.EMOJI_DATA.keys())
filtered_emoji_list=[]

#filtering emojis according to needs
common_words = [ "face",  "smile", "grin", "laugh", "joy", "walking","happy","hero","teacher","villain", "scientist",
"sad", "cry", "angry", "frown","kiss" , "heart",   "pizza", "hamburger", "coffee", "beer", "wine", "food", "drink",  "cat", 
"dog", "animal",  "sun", "moon", "star", "cloud", "rain", "weather",  "car", "bus", "train", "plane", "transport",   "phone",
"computer", "keyboard", "tech", "book", "pen", "pencil", "art","sport", "ball", "game", "music", "movie", "tv", "flag", "country",  "clap", "thumbs",  "peace", ]
for i in range(len(emoji_list)):
    for j in common_words:
        if j in emoji.demojize(emoji_list[i]):
            filtered_emoji_list.append(emoji.demojize(emoji_list[i]))

#removing problematic and exceptional emojis
crap_list=[':Japanese_application_button:',':Cook_Islands:',':black_cat:',':american_football:']
for i in crap_list:
    try:
        filtered_emoji_list.remove(i)
    except:
        pass

#changing required words to emojis
for i in range(len(seperated_words)):
    if(len(seperated_words[i])>=3):
        for j in  filtered_emoji_list :
            if(seperated_words[i][len(seperated_words[i])-1]=="s"):
               seperated_words[i]=seperated_words[i].rstrip("s")
            if(seperated_words[i] in emoji.demojize(j) and len(emoji.demojize(j))-len(seperated_words[i])<9):
                seperated_words[i]=emoji.demojize(j)
            if(seperated_words[i]=="love"):
                seperated_words[i]=":red_heart:"
            if(seperated_words[i]=="icecream"):
                seperated_words[i]=":ice_cream:"
print(seperated_words)

#creating final sentence           
final_sentence=""
for i in seperated_words:
    if (len(i)>=3) :
         final_sentence=final_sentence+emoji.emojize(i)+"  "
    else:
        final_sentence=final_sentence+i+" "
#printing result
print("emojified sentence")
print(final_sentence)
