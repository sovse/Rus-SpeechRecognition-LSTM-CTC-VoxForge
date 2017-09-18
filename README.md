# Rus_speech_recognition_LSTM_CTC_VoxForge
Это маленькая модель для Автоматического Распознования Речи русского языка, обученная на корпусе данных VoxForge(  2,9 ГБ).
Она использует два слоя  B-LSTM( рекурентная сеть с «длинной кратковременной памятью») по 128 нейронов и функцию потерь CTC (Нейросетевая темпоральная классификация).

Проверить работу можно запустив файл example.ipynd , он переводит речь из  двух аудио файлов с мужским и женским голосом в текст из обучающей выборки. Затем  можно попробовать распознать речь с микрофона.

Для начала обучения надо скачать с  VoxForge репозитория данные на локальную машину, этим занимается файл 
download_voxforge_data.ipynd . На диске должно быть свободно минимум 3Гб.

Файл train_lstm_ctc_voxforge_rus.ipynd обучает модель нейронной сети и сохраняет чекпоинты в папку  
\checkpoint1. По умолчанию, в этой папке лежит предобученная модель на 699 эпохе.

Add-my-wav.ipynb - Добовляет примеры txt и wav файлов надиктованные на Ваш локальный микрофон (использует pyaudio ). В нем надо набрать фразу на клавиатуре на русском языке, а затем произнести её в микрофон. 

Алгоритм работы:
Звуковой фаил wav формата разбивается на части по 10 мс, и преобразуется в 13 Mel Frequency Cepstral Coefficients (MFCCs) , они подаются на вход нейронной сетки, на выходе буквы русского алфавита + пробел и + пустой символ. Во время обучения оптимизируется функция потерь CTC.

## Requirements

- Python 2.7+
- Jupyter Notebook
- Tensorflow 1.0+
- Keras
- python_speech_features
- numpy
- scipy


An russian end-to-end model for Automatic Speech Recognition(ASR) on a small VoxForge dataset. It uses a CTC loss function and 2 layer B-LSTM Network.

Start by first running the "download_voxforge_data.ipynd" this downloads the data from the VoxForge repository for the specific speaker "Aaron". More data can be downloaded by making minor changes in the script.


Now, run the "train_lstm_ctc_voxforge_rus" to get the input features for speech recognition, Mel Frequency Cepstral Coefficients (MFCCs) are extracted. They are assembled into a batched format with the target character level annotations for subsequent training

 uses 2 layer bidirectional LSTM network to predict the transcriptions from the audio features. Every 1 epochs, an example batch is decoded and printed for comparision with the target.
