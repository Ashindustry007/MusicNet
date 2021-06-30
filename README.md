# MusicNet

Classical music generation using Sequential Deep learning Model.

Objectives:

The early 18th century evidenced the rise of classical piano music with a lot of legendary musicians like Beethoven. But with his demise, his creative intelligence is no more available. The prodigy who created master pieces like Moonlight Sonata and Fur Elise is no more creating any such master pieces. But fortunately, we have all his past records. Every great beauty in the nature has certain pattern in it and so does the thought process of a brilliant composer. So with enough data we can recognise the pattern of the composing methods of Beethoven and reproduce music like him.

Music Literature:

We are using the MIDI format of the music. It is basically a way of representing music in it’s most basic form. MIDI stands for Musical Instrument Digital Interface. It is commonly used as a standard to communicate between instruments by various manufacturers. When music is quantised it gives up Notes. Combination of notes make chords. And pattern of notes and chords make melodies. 
There are total 12 notes, i.e., A, A#, B, C, C#, D, D#, E, F, F#, G, G#. They are distributed over different octaves making total 128 unique frequencies of sound. So, basically we can use this info to train a model over 128 classes. 


Dataset :

The dataset consists of MIDI of 157 Classical pieces by Beethoven. Each classical piece can have multiple tracks, each track with hundreds and thousands of messages.
The messages basically look like this.
note_off channel=0 note=65 velocity=100 time=96
The above message says the note number 65 of channel 0 has been released with velocity 100 after at time 96. “note_on” means a note is being pressed and “note_off” means a note is being released. So before a “note_off” there has to be it’s respective “note_on”.

Data Processing :

The messages can’t be fed into the model directly so we have to extract the notes out of it and make an array of notes. That will work as our vector to feed into the sequential model. 
The predicted output will also be an array of notes, and now we have to convert back the note to stream format. We will use music21 to convert it back to MIDI and then a MIDI to WAV converter afterwards to play it in code. 
We will generally use Melody-RNN’s Encoder and Decoder Concept to process and de-process the data.


Model Development :

In this generation we are going to use the simple LSTM cells with Embedding layers. The LSTM cells are used to preserve the long-term dependencies. The embedding layer would have the vocabulary size as 130. The last dense cell hence has 130 classes to predict.

The classes are distributed as given below.
0-127 : All the notes
128 : note off
129 : skip a note
Total = 130 classes

The model architecture is as shown below.
 
![Screenshot 2021-06-28 014135](https://user-images.githubusercontent.com/44130583/124004109-515a0100-d9f5-11eb-9955-b7d8087c6310.png)

Results And Analysis :

The tunes obtained are still raw. The notes mimic Beethoven but don’t feel like him. It certainly adapted the melodic repetition of Beethoven but could not create patterns that would sound great.

Future Work :

The model architecture can be changed. The way we process only the notes can be changed to adapt more data into the model. The model might be taught to predict not only notes rather some additional facts to smoothen the predicted music. The MIDI to WAV conversion can be better keeping the conversion lossless. 
