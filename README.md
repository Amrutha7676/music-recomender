# music-recomender
import webbrowser
from textblob import TextBlob

MOOD_PLAYLISTS = {
    "positive": "https://www.youtube.com/playlist?list=PLFgquLnL59alCl_2TQvOiD5Vgm1hCaGSI",  
    "negative": "https://www.youtube.com/playlist?list=PLMC9KNkIncKtPzgY-5rmhvj7fax8fdxoj", 
    "neutral": "https://www.youtube.com/playlist?list=PL64ScZt1nduW6SY3GrrrY3n5rzf0XMFjE"   
}

def get_user_mood():
    """Ask the user how they are feeling."""
    user_input = input("🌟 How are you feeling today? Write a sentence: ")
    return user_input

def analyze_mood(text):
    """Analyze sentiment polarity and return mood category."""
    blob = TextBlob(text)
    polarity = blob.sentiment.polarity
    print(f"📊 Sentiment Polarity Score: {polarity:.2f}")

    if polarity > 0.3:
        return "positive"
    elif polarity < -0.3:
        return "negative"
    else:
        return "neutral"

def recommend_music(mood):
    """Open the appropriate playlist in the default browser."""
    print(f"\n🎶 Based on your mood ({mood}), here's a playlist for you!")
    url = MOOD_PLAYLISTS[mood]
    webbrowser.open(url)

def main():
    print("🎵 Welcome to the Mood-Based Music Recommender 🎵\n")
    user_text = get_user_mood()
    mood = analyze_mood(user_text)
    recommend_music(mood)

if __name__ == "__main__":
    main()
