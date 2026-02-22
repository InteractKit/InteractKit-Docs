# Interruption Handling

When VAD detects speech while the bot is talking, audio delivery is suspended. If STT confirms real speech, the interruption is committed and the bot stops speaking. Otherwise, buffered audio resumes playback.

This provides natural turn-taking without cutting off the bot on background noise.
