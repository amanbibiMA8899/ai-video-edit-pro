
import os
from gtts import gTTS
from moviepy.editor import ImageClip, AudioFileClip

def generate_ai_video(text_script, image_path, output_filename="ai_video.mp4"):
    print("1. Text se Audio ban raha hai...")
    # Text ko MP3 voiceover mein convert karein
    tts = gTTS(text=text_script, lang='ur', slow=False)
    audio_file = "temp_voice.mp3"
    tts.save(audio_file)

    print("2. Video generate ho rahi hai...")
    # Audio aur Image ko mila kar video banayein
    audio_clip = AudioFileClip(audio_file)
    video_clip = ImageClip(image_path).set_duration(audio_clip.duration)
    video_clip = video_clip.set_audio(audio_clip)

    # Final Video Export
    video_clip.write_videofile(
        output_filename, 
        fps=24, 
        codec="libx264", 
        audio_codec="aac"
    )

    # Clean up temporary files
    audio_clip.close()
    video_clip.close()
    if os.path.exists(audio_file):
        os.
