### Install required packages
```
# build packages
apt install autoconf automake build-essential cmake git-core libass-dev libfreetype6-dev libgnutls28-dev libmp3lame-dev libsdl2-dev libtool libva-dev libvdpau-dev libvorbis-dev libxcb1-dev libxcb-shm0-dev libxcb-xfixes0-dev meson ninja-build pkg-config texinfo wget yasm zlib1g-dev
# ffmpeg dependencies
apt install libx264-dev libx265-dev libnuma-dev libvpx-dev libfdk-aac-dev libopus-dev libaom-dev libdav1d-dev libunistring-dev libyuv-dev
# to build .deb
apt install devscripts debhelper
```
### Build rockchip mpp
```
git clone https://github.com/rockchip-linux/mpp.git -b develop
cd mpp
cmake CMakeLists.txt
make
make install
cd ..
```
### Build linux-rga-multi
```
git clone https://github.com/tsukumijima/librga-rockchip.git
cd librga-rockchip
debuild -us -uc -b && cp -a ../*.deb ./
dpkg -i librga*.deb
cd ..
```
### Build ffmpeg
```
git clone https://github.com/hbiyik/FFmpeg.git
cd FFmpeg

PATH="$HOME/bin:$PATH" PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig" ./configure \
	--prefix="$HOME/ffmpeg_build" \
	--pkg-config-flags="--static" \
	--extra-cflags="-I$HOME/ffmpeg_build/include" \
	--extra-ldflags="-L$HOME/ffmpeg_build/lib" \
	--extra-libs="-lpthread -lm" \
	--ld="g++" \
	--bindir="$HOME/bin" \
	--enable-gpl \
	--enable-gnutls \
	--enable-libaom \
	--enable-libass \
	--enable-libfdk-aac \
	--enable-libfreetype \
	--enable-libmp3lame \
	--enable-libopus \
	--enable-libdav1d \
	--enable-libvorbis \
	--enable-libvpx \
	--enable-libx264 \
	--enable-libx265 \
	--enable-nonfree \
	--enable-rkmpp \
	--enable-version3 \
	--enable-libdrm && \
PATH="$HOME/bin:$PATH" make -j4 && \
make install
```
And here it is
```
./ffmpeg -codecs | grep rkmpp
```
Outputs:
```
ffmpeg version e243e8d001 Copyright (c) 2000-2023 the FFmpeg developers
  built with gcc 12 (Ubuntu 12.3.0-1ubuntu1~23.04)
  configuration: --prefix=/root/ffmpeg_build --pkg-config-flags=--static --extra-cflags=-I/root/ffmpeg_build/include --extra-ldflags=-L/root/ffmpeg_build/lib --extra-libs='-lpthread -lm' --ld=g++ --bindir=/root/bin --enable-gpl --enable-gnutls --enable-libaom --enable-libass --enable-libfdk-aac --enable-libfreetype --enable-libmp3lame --enable-libopus --enable-libdav1d --enable-libvorbis --enable-libvpx --enable-libx264 --enable-libx265 --enable-nonfree --enable-rkmpp --enable-version3 --enable-libdrm
  libavutil      58.  2.100 / 58.  2.100
  libavcodec     60.  3.100 / 60.  3.100
  libavformat    60.  3.100 / 60.  3.100
  libavdevice    60.  1.100 / 60.  1.100
  libavfilter     9.  3.100 /  9.  3.100
  libswscale      7.  1.100 /  7.  1.100
  libswresample   4. 10.100 /  4. 10.100
  libpostproc    57.  1.100 / 57.  1.100
 DEV.L. av1                  Alliance for Open Media AV1 (decoders: av1_rkmpp_decoder libdav1d libaom-av1 av1 ) (encoders: libaom-av1 )
 DEV.L. h263                 H.263 / H.263-1996, H.263+ / H.263-1998 / H.263 version 2 (decoders: h263_rkmpp_decoder h263 h263_v4l2m2m ) (encoders: h263 h263_v4l2m2m )
 DEV.LS h264                 H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10 (decoders: h264_rkmpp_decoder h264 h264_v4l2m2m ) (encoders: h264_rkmpp_encoder libx264 libx264rgb h264_v4l2m2m h264_vaapi )
 DEV.L. hevc                 H.265 / HEVC (High Efficiency Video Coding) (decoders: hevc_rkmpp_decoder hevc hevc_v4l2m2m ) (encoders: hevc_rkmpp_encoder libx265 hevc_v4l2m2m hevc_vaapi )
 DEV.L. mpeg1video           MPEG-1 video (decoders: mpeg1_rkmpp_decoder mpeg1video mpeg1_v4l2m2m )
 DEV.L. mpeg2video           MPEG-2 video (decoders: mpeg2_rkmpp_decoder mpeg2video mpegvideo mpeg2_v4l2m2m ) (encoders: mpeg2video mpeg2_vaapi )
 DEV.L. mpeg4                MPEG-4 part 2 (decoders: mpeg4_rkmpp_decoder mpeg4 mpeg4_v4l2m2m ) (encoders: mpeg4 mpeg4_v4l2m2m )
 DEV.L. vp8                  On2 VP8 (decoders: vp8_rkmpp_decoder vp8 vp8_v4l2m2m libvpx ) (encoders: vp8_rkmpp_encoder libvpx vp8_v4l2m2m vp8_vaapi )
 DEV.L. vp9                  Google VP9 (decoders: vp9_rkmpp_decoder vp9 vp9_v4l2m2m libvpx-vp9 ) (encoders: libvpx-vp9 vp9_vaapi )
```
