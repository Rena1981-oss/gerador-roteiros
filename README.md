from flask import Flask, render_template, request
import openai
from youtube_transcript_api import YouTubeTranscriptApi

app = Flask(__name__)

openai.api_key = "SUA_API_KEY"  # Coloque sua chave da OpenAI aqui

@app.route("/", methods=["GET", "POST"])
def home():
    if request.method == "POST":
        palavra_chave = request.form["palavra-chave"]
        transcript = gerar_transcricao(palavra_chave)
        roteiro = reescrever_roteiro(transcript)
        return render_template("index.html", roteiro=roteiro)
    return render_template("index.html")

def gerar_transcricao(palavra_chave):
    # Aqui vai o código para buscar a transcrição do vídeo
    return "Exemplo de transcrição"

def reescrever_roteiro(transcript):
    # Reescrevendo o roteiro com OpenAI
    response = openai.Completion.create(
        engine="text-davinci-003", 
        prompt=f"Reescreva o seguinte roteiro: {transcript}",
        max_tokens=150
    )
    return response.choices[0].text.strip()

if __name__ == "__main__":
    app.run(debug=True)
