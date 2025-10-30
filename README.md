# 🎧 DJ System using OSC and Pure Data

## 👥 Team Members
- **David Felipe Hurtado Marroquín**
- **Juan David Troncoso**

---

## 📖 Project Description
This project is a **DJ system** created using **OSC Controller** and **Pure Data (PD)**.  
The goal was to design an interactive system that allows users to control and mix sounds using different widgets from the OSC mobile app, such as sliders and buttons. Each control in the OSC interface sends messages to Pure Data, producing real-time audio effects similar to those used by a DJ.

The system lets the user manipulate:
- **Volume** (for two decks)
- **Low-pass and high-pass filters**
- **Reverb and delay effects**
- **Synchronization controls (Sync and SyncStop)**
- **Drum sounds:** *Kick, Snare, and Cymbal*

All controls communicate via **Open Sound Control (OSC)** messages, ensuring smooth interaction between the mobile app and the Pure Data patch.

### 🎥 Video Demonstration
**[Watch the project demo on YouTube](https://www.youtube.com/watch?v=MS1P-mApcHQ)**

[![Video Demo](https://img.shields.io/badge/YouTube-Watch%20Demo-red?style=for-the-badge&logo=youtube)](https://www.youtube.com/watch?v=MS1P-mApcHQ)

---

## ⚙️ How It Works
1. The OSC Controller app connects to Pure Data through a **UDP port (5580)**.  
2. Each widget in the OSC layout sends data such as volume, filter values, or button states.  
3. Pure Data receives and interprets these messages using `netreceive`, `oscparse`, and `list trim`.  
4. The received data controls different parts of the audio chain:
   - **Volume sliders** adjust the amplitude of each deck.
   - **Filter sliders** modify the cutoff frequencies for low-pass and high-pass effects.
   - **Reverb** and **Delay** sliders add spatial effects to the sound.
   - **Sync buttons** allow both decks to play or stop simultaneously.
   - **Kick, Snare, and Cymbal** buttons trigger synthesized drum sounds created within PD.
5. The user can mix, sync, and modify the sound in real time, creating an electronic music experience similar to a professional DJ setup.

---

## 💡 Design Justification
We decided to implement this system using Pure Data because:
- It provides **real-time audio processing** and **visual programming**, making it ideal for prototyping interactive systems.
- OSC allows **intuitive communication** between mobile devices and PD, offering flexibility for live performance.
- The project demonstrates **interaction design principles**, combining multiple input types (sliders, buttons) to produce immediate, meaningful auditory feedback.
- Using both decks and drum synthesis modules (Kick, Snare, Cymbal) adds creative possibilities for live music composition and performance.

---

## 🧰 Tools and Technologies
- **Pure Data (PD)**
- **OSC Controller (Mobile App)**
- **UDP Communication Protocol**
- **Audio synthesis modules** (reverb, filters, delay, percussion)

---

## ▶️ Video


---

## 📁 Repository Structure