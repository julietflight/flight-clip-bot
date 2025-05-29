{\rtf1\ansi\ansicpg1252\cocoartf2822
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\paperw11900\paperh16840\margl1440\margr1440\vieww11520\viewh8400\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 import streamlit as st\
import requests\
import tempfile\
import moviepy.editor as mp\
from typing import List\
import os\
from PIL import Image\
from io import BytesIO\
import json\
import uuid\
import whisper\
\
DOAC_API_URL = "https://doac-search-app-final-821517401106.europe-west1.run.app/search"\
PEXELS_API_KEY = "YOUR_PEXELS_API_KEY"  # Replace with your API key\
PEXELS_VIDEO_SEARCH_URL = "https://api.pexels.com/videos/search"\
PEXELS_IMAGE_SEARCH_URL = "https://api.pexels.com/v1/search"\
\
st.set_page_config(layout="wide")\
st.title("\uc0\u55356 \u57260  AI Clip Editor + B-Roll Generator + SEO & Branding")\
\
# Session State for Project Saving\
if "saved_projects" not in st.session_state:\
    st.session_state.saved_projects = \{\}\
\
# Sidebar: Branding options\
st.sidebar.header("Brand Kit")\
logo_file = st.sidebar.file_uploader("Upload Logo (PNG)", type=["png"])\
subtitle_style = st.sidebar.selectbox("Subtitle Style", ["White on Black", "Yellow on Transparent", "Bold White Shadow"])\
logo_position = st.sidebar.selectbox("Logo Placement", ["Top Right", "Top Left", "Bottom Right", "Bottom Left"])\
font_size = st.sidebar.slider("Subtitle Font Size", 16, 48, 24)\
font_color = st.sidebar.color_picker("Subtitle Font Color", "#FFFFFF")\
\
# Upload section\
st.markdown("Upload a podcast video + transcript and we'll auto-generate highlight clips, stitch them with stock footage, apply branding, and suggest SEO keywords!")\
video_file = st.file_uploader("Upload podcast video (MP4)", type=["mp4"])\
transcript_text = st.text_area("Paste transcript text here")\
query = st.text_input("Search prompt (e.g. 'funniest moment', 'inspirational quote')", value="funniest moment")\
\
if st.button("Suggest Clip Queries with GPT"):\
    with st.spinner("Analyzing transcript and generating suggestions..."):\
        suggestions = ["funniest moment", "inspirational quote", "unexpected story"]\
        st.success("Suggested prompts: " + ", ".join(suggestions))\
\
guest_name = st.text_input("Guest name (for baby photos, auditions, etc.)")\
broll_keywords = st.text_input("Additional B-roll search keywords (comma-separated)")\
\
headers = \{"Authorization": PEXELS_API_KEY\}\
\
def fetch_pexels_videos(keywords):\
    videos = []\
    for keyword in keywords:\
        params = \{"query": keyword.strip(), "per_page": 1\}\
        response = requests.get(PEXELS_VIDEO_SEARCH_URL, headers=headers, params=params)\
        if response.status_code == 200:\
            data = response.json()\
            for video in data.get("videos", []):\
                videos.append(video["video_files"][0]["link"])\
    return videos\
\
def fetch_guest_footage(guest):\
    search_links = [\
        f"https://www.youtube.com/results?search_query=\{guest\}+baby+photo",\
        f"https://www.youtube.com/results?search_query=\{guest\}+audition",\
        f"https://twitter.com/search?q=\{guest\}%20audition",\
        f"https://www.tiktok.com/search?q=\{guest\}%20audition"\
    ]\
    return search_links\
\
def generate_seo_suggestions(transcript):\
    return ["#Motivation", "#PodcastClips", "Guest Name + Topic", "Shorts", "Reel"]\
\
def save_project(name, data):\
    st.session_state.saved_projects[name] = data\
\
def load_project(name):\
    return st.session_state.saved_projects.get(name)\
\
project_name = st.text_input("Project Name")\
if st.button("\uc0\u55357 \u56510  Save Project"):\
    if transcript_text and video_file:\
        save_project(project_name, \{\
            "transcript": transcript_text,\
            "query": query,\
            "guest_name": guest_name,\
            "broll_keywords": broll_keywords\
        \})\
        st.success(f"Saved project '\{project_name\}'")\
\
if st.selectbox("\uc0\u55357 \u56514  Load Project", ["Select"] + list(st.session_state.saved_projects.keys())) != "Select":\
    loaded = load_project(project_name)\
    transcript_text = loaded["transcript"]\
    query = loaded["query"]\
    guest_name = loaded["guest_name"]\
    broll_keywords = loaded["broll_keywords"]\
\
if st.button("Generate Final Reel"):\
    if video_file and transcript_text and query:\
        with st.spinner("Searching transcript with DOAC AI..."):\
            response = requests.post(\
                DOAC_API_URL,\
                json=\{"query": query, "transcript": transcript_text\}\
            )\
\
            if response.status_code != 200:\
                st.error("DOAC search failed. Please try again.")\
            else:\
                results = response.json().get("results", [])\
\
                if not results:\
                    st.warning("No relevant clips found. Try a different prompt.")\
                else:\
                    st.success(f"Found \{len(results)\} highlight(s). Select timeline order below.")\
\
                    with tempfile.NamedTemporaryFile(delete=False, suffix=".mp4") as tmp:\
                        tmp.write(video_file.read())\
                        tmp_path = tmp.name\
\
                    original_clip = mp.VideoFileClip(tmp_path)\
                    clip_options = []\
\
                    for i, result in enumerate(results):\
                        start = max(0, result['start'] - 5)\
                        end = result['end'] + 5\
                        label = f"Clip \{i+1\}: \{start\}-\{end\} sec"\
                        clip_options.append((label, start, end, transcript_text[result['start']:result['end']]))\
\
                    ordered_clips = st.multiselect("\uc0\u55358 \u56809  Select & Order Clips for Final Timeline", [c[0] for c in clip_options], default=[c[0] for c in clip_options])\
\
                    final_clips = []\
                    subtitles = []\
                    for label in ordered_clips:\
                        for c in clip_options:\
                            if c[0] == label:\
                                subclip = original_clip.subclip(c[1], min(c[2], original_clip.duration))\
                                final_clips.append(subclip)\
                                subtitles.append(c[3])\
\
                    search_terms = []\
                    if broll_keywords:\
                        search_terms.extend(broll_keywords.split(","))\
                    if guest_name:\
                        search_terms.append(f"\{guest_name\} baby photo")\
                        search_terms.append(f"\{guest_name\} audition")\
\
                    broll_video_links = fetch_pexels_videos(search_terms)\
                    for link in broll_video_links:\
                        try:\
                            clip = mp.VideoFileClip(link).subclip(0, 3)\
                            final_clips.append(clip)\
                        except:\
                            continue\
\
                    final_video = mp.concatenate_videoclips(final_clips, method="compose")\
\
                    overlays = [final_video]\
                    if logo_file:\
                        logo_temp = tempfile.NamedTemporaryFile(delete=False, suffix=".png")\
                        logo_temp.write(logo_file.read())\
                        logo_temp.flush()\
                        logo_img = mp.ImageClip(logo_temp.name).set_duration(final_video.duration).resize(height=80)\
\
                        pos_dict = \{\
                            "Top Right": (final_video.w - 100, 10),\
                            "Top Left": (10, 10),\
                            "Bottom Right": (final_video.w - 100, final_video.h - 90),\
                            "Bottom Left": (10, final_video.h - 90)\
                        \}\
                        logo_img = logo_img.set_pos(pos_dict[logo_position])\
                        overlays.append(logo_img)\
\
                    for i, subtitle in enumerate(subtitles):\
                        subtitle_clip = mp.TextClip(subtitle, fontsize=font_size, color=font_color)\
                        subtitle_clip = subtitle_clip.set_duration(final_clips[i].duration).set_pos(('center', 'bottom'))\
                        subtitle_clip = subtitle_clip.set_start(sum(c.duration for c in final_clips[:i]))\
                        overlays.append(subtitle_clip)\
\
                    final_video = mp.CompositeVideoClip(overlays)\
\
                    output_path = "final_reel.mp4"\
                    final_video.write_videofile(output_path, codec="libx264")\
                    st.video(output_path)\
\
                    st.subheader("\uc0\u55357 \u56589  Suggested SEO Tags")\
                    for tag in generate_seo_suggestions(transcript_text):\
                        st.code(tag)\
\
                    if guest_name:\
                        st.subheader("\uc0\u55356 \u57104  Guest Clip Sources")\
                        for link in fetch_guest_footage(guest_name):\
                            st.markdown(f"- [\uc0\u55357 \u56599  \{link\}](\{link\})")\
    else:\
        st.warning("Please upload a video, paste the transcript, and enter a search prompt.")\
}