OBS Fork Project Summary

Project Goal

Creating a lightweight version of OBS Studio that focuses on real-time audio processing with VST plugin support, removing video recording capabilities except what's needed to decode audio from video sources.

Unique Value Proposition
This project fills a gap that existing software doesn't address well:
    • Real-time audio processor for video sources 
    • Lower latency than traditional DAWs 
    • Simpler than full OBS Studio 
    • More capable than basic audio software 
    • Perfect for live movie watching, gaming, streaming, video calls with audio enhancement 

Background & Motivation

    • Currently uses OBS Studio specifically for its VST plugin capability for real-time audio enhancement 
    • Uses Tokyo Dawn Record's TDR Nova GE VST-Plugin as dynamic audio compressor and equalizer 
    • Key advantage of OBS over DAWs like Reaper: Much lower latency when watching movies with real-time VST processing 
    • OBS is optimized for live streaming/recording with minimal processing delays, while DAWs have higher latency buffers for production stability 

Technical Requirements
    • Real-time audio processing with VST plugin support 
    • Ability to extract audio from video sources 
    • Minimal latency (OBS's key advantage) 
    • Remove video recording/encoding components 
    • Maintain existing VST integration functionality 
Key OBS Source Files Identified
Core Audio Processing
    • libobs/audio-io.c - Main audio I/O handling 
    • libobs/audio-monitoring/ - Audio monitoring system 
    • libobs/media-io/audio-io.c - Lower-level audio operations 
    • libobs/media-io/audio-resampler-ffmpeg.c - Audio resampling 
VST Plugin Integration
    • plugins/obs-filters/vst-filter.cpp - Main VST plugin host 
    • plugins/obs-filters/vst-filter.h - VST filter definitions 
    • plugins/obs-filters/CMakeLists.txt - Build configuration for filters 
Audio Sources (Keep for Video Audio Extraction)
    • plugins/obs-ffmpeg/ffmpeg-source.c - Media file sources 
    • plugins/obs-ffmpeg/obs-ffmpeg-source.h - FFmpeg source headers 
Audio Filters & Processing
    • plugins/obs-filters/noise-suppress-filter.c 
    • plugins/obs-filters/gain-filter.c 
    • plugins/obs-filters/compressor-filter.c 
    • plugins/obs-filters/expander-filter.c 
Core Architecture
    • libobs/obs.c - Main OBS core initialization 
    • libobs/obs-source.c - Source management (audio sources) 
    • libobs/obs-output.c - Output handling 
    • libobs/callback/ - Event system 
Components to Remove
    • Most of libobs-opengl/ and libobs-d3d11/ (video rendering) 
    • plugins/win-capture/, plugins/linux-capture/ (video capture) 
    • Most UI components in UI/ except basic controls 
VST Implementation Architecture
    • VST filters follow OBS's audio filter pattern 
    • Key function: filter_audio callback processes audio through VST plugins 
    • Audio flow: Input → VST Filter Chain → Output 
    • Supports chaining multiple VST filters 
    • Handles VST plugin loading, parameter management, and real-time processing 
Data Flow Pattern
1. Audio comes in → obs_audio_data structure
2. Convert to VST format → float arrays
3. Process through VST → plugin->processReplacing()
4. Convert back → obs_audio_data structure
5. Return processed audio
Recommended Next Steps
    1. Get OBS building locally 
    2. Explore codebase structure using provided file paths 
    3. Make small changes to confirm build process works 
    4. Study the audio pipeline and VST integration 
    5. Use provided search commands to trace VST implementation 
    6. Focus on understanding the filter_audio callback pattern 
Search Commands for Code Exploration
# Find VST-related files
find . -name "*vst*" -type f
grep -r "vst" --include="*.cpp" --include="*.c" --include="*.h" .

# Find main VST processing function
grep -n "filter_audio" plugins/obs-filters/*.cpp

# Find VST plugin loading code
grep -n "LoadLibrary\|dlopen" plugins/obs-filters/*.cpp

# Find VST parameter handling
grep -n "setParameter\|getParameter" plugins/obs-filters/*.cpp
Technology Stack
    • Language: C++ with some C components 
    • Build System: CMake 
    • UI Framework: Qt (to be simplified) 
    • VST Integration: VST SDK 
    • Video Processing: FFmpeg (for audio extraction only) 

Current Status
    • OBS fork created but no development work started yet 

OBS Studio <https://obsproject.com>
===================================

.. image:: https://github.com/obsproject/obs-studio/actions/workflows/push.yaml/badge.svg?branch=master
   :alt: OBS Studio Build Status - GitHub Actions
   :target: https://github.com/obsproject/obs-studio/actions/workflows/push.yaml?query=branch%3Amaster

.. image:: https://badges.crowdin.net/obs-studio/localized.svg
   :alt: OBS Studio Translation Project Progress
   :target: https://crowdin.com/project/obs-studio

.. image:: https://img.shields.io/discord/348973006581923840.svg?label=&logo=discord&logoColor=ffffff&color=7389D8&labelColor=6A7EC2
   :alt: OBS Studio Discord Server
   :target: https://obsproject.com/discord

What is OBS Studio?
-------------------

OBS Studio is software designed for capturing, compositing, encoding,
recording, and streaming video content, efficiently.

It's distributed under the GNU General Public License v2 (or any later
version) - see the accompanying COPYING file for more details.

Quick Links
-----------

- Website: https://obsproject.com

- Help/Documentation/Guides: https://github.com/obsproject/obs-studio/wiki

- Forums: https://obsproject.com/forum/

- Build Instructions: https://github.com/obsproject/obs-studio/wiki/Install-Instructions

- Developer/API Documentation: https://obsproject.com/docs

- Donating/backing/sponsoring: https://obsproject.com/contribute

- Bug Tracker: https://github.com/obsproject/obs-studio/issues

Contributing
------------

- If you would like to help fund or sponsor the project, you can do so
  via `Patreon <https://www.patreon.com/obsproject>`_, `OpenCollective
  <https://opencollective.com/obsproject>`_, or `PayPal
  <https://www.paypal.me/obsproject>`_.  See our `contribute page
  <https://obsproject.com/contribute>`_ for more information.

- If you wish to contribute code to the project, please make sure to
  read the coding and commit guidelines:
  https://github.com/obsproject/obs-studio/blob/master/CONTRIBUTING.rst

- Developer/API documentation can be found here:
  https://obsproject.com/docs

- If you wish to contribute translations, do not submit pull requests.
  Instead, please use Crowdin.  For more information read this page:
  https://obsproject.com/wiki/How-To-Contribute-Translations-For-OBS

- Other ways to contribute are by helping people out with support on
  our forums or in our community chat.  Please limit support to topics
  you fully understand -- bad advice is worse than no advice.  When it
  comes to something that you don't fully know or understand, please
  defer to the official help or official channels.
