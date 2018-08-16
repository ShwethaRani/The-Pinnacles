import os
import tempfile
import subprocess
from nltk.corpus import wordnet 

def ocr(path):
    temp = tempfile.NamedTemporaryFile(delete=False)
    process = subprocess.Popen(['tesseract', path, temp.name], stdout=subprocess.PIPE, stderr=subprocess.STDOUT)
    process.communicate()
    with open(temp.name + '.txt', 'r') as handle:
        contents = handle.read()
    os.remove(temp.name + '.txt')
    os.remove(temp.name)
    return contents
str = ocr('image.png')
print(str)

//Synonyms for the word
synonyms = []
for syn in wordnet.synsets(str):
    for lemma in syn.lemmas():
        synonyms.append(lemma.name())
print(synonyms)

//Antonyms for the word
from nltk.corpus import wordnet
antonyms = []
for syn in wordnet.synsets(str):
    for l in syn.lemmas():
        if l.antonyms():
            antonyms.append(l.antonyms()[0].name())
print(antonyms)

