# Perfecting Your ChatGPT Prompts

## Section 1: The basics

- Sample 01: Create a project in ChatGPT callBirthday Party Planning
---
- Sample 02: Create a new chat and type `Tell me 5 interesting facts about coffee`
- Sample 03: Could you expand fact number 1 into a short story, told from the point of view of a goatherd
- Sample 04: Rewrite the story as a poem
---
- Sample 05: Open a new chat, Generate an image of a four-story house in the mointains, with a waterfall nearby
- Sample 06: Edit the image,select the house an prompt `Make the house bright yellow, with red shutters`
- Sample 06.1: Edit again the images, select a spot and prompt `Draw here 3 white dogs playing near the house`


---
- Sample 07: Open a new chat, and paste the image of an interior house and prompt `I like something about this interior, but I can't quite figure out what. Help me deconstruct the different aspects of this image`.
- Sample 08: Paste another image in the same chat a waterfall and prompt `Where in the world was this picture taken`.

---
- Sample 09: Open a new chat, use the search option, and prompt What's the weather like in Detroit Michigan
- Sample 10: Prompt: `Describe the biggest stock market movements in the past 3 days and come up with a possible explanation for each`

---
- Sample 11: 
 - Create a spredsheet with first column in english messages
 	- Buy Now!
 	- Hurry! The Sale Ends in less than 24 hours!
 	- Speak with our Virtual Agent
 	- View my shopping cart
 	- See related Products
 - Add a header in other columns mentioning the new language like
 	spanish, japannese, italian, french, finnish
 - Open a new chat, upload the file and prompt: `Fill in the rest of this spreadsheet with the appropiate translations`	. Use a reasoning model (for this sample 04-mini-hight)

- Sample 11.1: Chanche the python, to read the google api to tranlate the messages

### Original Script
```python
import pandas as pd

# Load the original spreadsheet
input_path = '/mnt/data/Web Page Messages.xlsx'
df = pd.read_excel(input_path)

# Fill in translations
translations = [
    {
        "Spanish": "¡Compra ahora!",
        "Japannese": "今すぐ購入！",
        "Italian": "Acquista ora!",
        "French": "Achetez maintenant !",
        "Finnish": "Osta nyt!"
    },
    {
        "Spanish": "¡Apresúrate! ¡La venta termina en menos de 24 horas!",
        "Japannese": "急いで！セールは24時間以内に終了します！",
        "Italian": "Affrettati! La svendita termina tra meno di 24 ore!",
        "French": "Dépêche-toi ! La vente se termine dans moins de 24 heures !",
        "Finnish": "Kiirehdi! Ale päättyy alle 24 tunnissa!"
    },
    {
        "Spanish": "Habla con nuestro agente virtual",
        "Japannese": "バーチャルエージェントと話す",
        "Italian": "Parla con il nostro agente virtuale",
        "French": "Discutez avec notre agent virtuel",
        "Finnish": "Puhu virtuaalisen agenttimme kanssa"
    },
    {
        "Spanish": "Ver mi carrito de compras",
        "Japannese": "マイショッピングカートを見る",
        "Italian": "Visualizza il mio carrello",
        "French": "Voir mon panier",
        "Finnish": "Näytä ostoskorini"
    },
    {
        "Spanish": "Ver productos relacionados",
        "Japannese": "関連製品を見る",
        "Italian": "Vedi prodotti correlati",
        "French": "Voir les produits associés",
        "Finnish": "Katso liittyvät tuotteet"
    }
]

# Apply translations to the DataFrame
for idx, trans in enumerate(translations):
    for lang, text in trans.items():
        df.at[idx, lang] = text

# Save to a new Excel file
output_path = '/mnt/data/Web Page Messages Translated.xlsx'
df.to_excel(output_path, index=False)

# Display the translated DataFrame to the user
import ace_tools as tools; tools.display_dataframe_to_user(name="Translated Messages", dataframe=df)

print(f"[Download the translated spreadsheet]({output_path})")

```

### New Script
```python
import pandas as pd
from google.cloud import translate_v2 as translate
import os

# Ensure you have set the GOOGLE_APPLICATION_CREDENTIALS environment variable
# to point to your service account key JSON file:
# os.environ["GOOGLE_APPLICATION_CREDENTIALS"] = "/path/to/your/key.json"

# Load the original spreadsheet
input_path = '/mnt/data/Web Page Messages.xlsx'
df = pd.read_excel(input_path)

# Initialize the Translate client
translate_client = translate.Client()

# Map your DataFrame language columns to Google Translate codes
lang_codes = {
    'Spanish': 'es',
    'Japannese': 'ja',  # Adjust if your header is 'Japanese'
    'Italian': 'it',
    'French': 'fr',
    'Finnish': 'fi'
}

# Detect the source column (assumed to be the first column)
source_col = df.columns[0]

# Translate each message into the target languages
for idx, row in df.iterrows():
    text = row[source_col]
    for lang, code in lang_codes.items():
        translated = translate_client.translate(text, target_language=code)
        df.at[idx, lang] = translated['translatedText']

# Save to a new Excel file
output_path = '/mnt/data/Web Page Messages Translated.xlsx'
df.to_excel(output_path, index=False)

# Display the translated DataFrame
import ace_tools as tools; tools.display_dataframe_to_user(name="Translated Messages with Google API", dataframe=df)

print(f"[Download the translated spreadsheet]({output_path})")

```

---
- Sample 12: (Use o3) use the prompt `If someone has $1000 to invest, what are the best options assuming we want to protect our principal and also make a reasonable return over 10 years. Run some possible scenarios with concrete numbers`


---

## Section 2:



## Resources 

- [Course][https://learning.oreilly.com/live-events/perfecting-your-chatgpt-prompts/0642572007492/0642572016132/]
- [Slides][https://on24static.akamaized.net/event/48/83/51/2/rt/1/documents/resourceList1745844093951/perfectingyourpromptsslides11745844093951.pdf]
- [Markdown Cheat Sheet](https://www.markdownguide.org/cheat-sheet/)
- [Evaluating model performance](https://platform.openai.com/docs/guides/evals)
- []()
- []()