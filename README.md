# Music Genre Prediction Model

A Streamlit application that predicts the genre of an uploaded audio file using a TensorFlow/Keras model and mel-spectrogram audio features.

## Features

- Upload `.wav` or `.mp3` audio files.
- Extract mel-spectrogram features with `librosa`.
- Predict one of ten music genres:
  `blues`, `classical`, `country`, `disco`, `hiphop`, `jazz`, `metal`, `pop`, `reggae`, and `rock`.
- Display the predicted genre, confidence score, and top three predictions.
- Cache the trained model in memory with Streamlit so it is not reloaded on every interaction.

## Project Structure

```text
.
|-- app.py                  # Streamlit user interface and inference logic
|-- preprocessing.py        # Audio loading and mel-spectrogram preprocessing
|-- music_genre_model2.h5   # Trained TensorFlow/Keras model
|-- requirements.txt        # Python dependencies
|-- runtime.txt             # Project Python runtime declaration
`-- train.ipynb             # Model training notebook
```

## Run Locally

Use Python 3.11 or Python 3.12. TensorFlow 2.20.0 is not compatible with Python 3.14.

1. Clone the repository and open its directory:

```bash
git clone https://github.com/<your-username>/Music-Genre-Prediction-Model.git
cd Music-Genre-Prediction-Model
```

2. Create and activate a virtual environment:

   **Windows PowerShell**

   ```powershell
   py -3.11 -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

   **macOS/Linux**

   ```bash
   python3.11 -m venv .venv
   source .venv/bin/activate
   ```

3. Install the dependencies:

   ```bash
   python -m pip install --upgrade pip
   python -m pip install -r requirements.txt
   ```

4. Start the application:

   ```bash
   streamlit run app.py
   ```

   Streamlit will print a local URL, usually `http://localhost:8501`.

## Deploy on Streamlit Community Cloud

1. Push the repository to GitHub.
2. Create a new app in Streamlit Community Cloud.
3. Select the repository, the `main` branch, and `app.py` as the entrypoint.
4. In **Advanced settings**, select Python **3.12** or another supported version compatible with the pinned dependencies. Do not select Python 3.14 because TensorFlow 2.20.0 has no Python 3.14 wheel.
5. Deploy or reboot the app after changing the Python version.

The model file `music_genre_model2.h5` must remain in the repository root because `app.py` loads it with a relative path.

## How Prediction Works

1. The uploaded audio is loaded at a sample rate of 22,050 Hz.
2. The audio is divided into three-second segments.
3. Each segment is converted to a mel spectrogram with 128 mel bands.
4. Features are padded or trimmed to the model input shape `(128, 128, 1)`.
5. The model predicts each segment, and the segment predictions are averaged.
6. The highest-probability genre is shown with the top three probabilities.

## Dependencies

The main packages are:

- Streamlit for the web interface
- TensorFlow/Keras for model inference
- Librosa and SoundFile for audio processing
- NumPy, pandas, Matplotlib, and scikit-learn for the machine-learning environment

Exact versions are defined in [requirements.txt](requirements.txt).

## Notes

- This is an inference application; training is documented in `train.ipynb`.
- Predictions depend on the quality, duration, and characteristics of the uploaded recording.
- The confidence value is the model's probability estimate, not a guarantee of correctness.