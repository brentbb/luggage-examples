include /usr/local/share/luggage/luggage.make

TITLE=VLC
REVERSE_DOMAIN=com.example.corp
PACKAGE_VERSION=1.1.9
# run make with ARCH=PowerPC to build the PPC version
ARCH=i386
PAYLOAD=undmg-applications-vlc \
		pack-user-template-plist-org.videolan.vlc.plist

VLC_FILE=vlc-${PACKAGE_VERSION}.dmg
ifeq (${ARCH},PowerPC)
	VLC_FILE=vlc-${PACKAGE_VERSION}-powerpc.dmg
	TITLE=VLC-PowerPC
endif

# using mirror from Montreal	
VLC_URL=http://iweb.dl.sourceforge.net/project/vlc/${PACKAGE_VERSION}/macosx/${VLC_FILE}
SCRATCH_MOUNT=${SCRATCH_D}/dmgmount

undmg-applications-vlc:	l_Applications
	curl -O ${VLC_URL}
	@sudo mkdir ${SCRATCH_MOUNT}
	@sudo hdiutil attach ${VLC_FILE} -mountpoint ${SCRATCH_MOUNT}
	@sudo ${CP} -R ${SCRATCH_MOUNT}/VLC.app ${WORK_D}/Applications
	@sudo chown -R root:admin ${WORK_D}/Applications/VLC.app
	@sudo hdiutil detach ${SCRATCH_MOUNT}
	# since the downloaded file has the same name as what we might be building...
	@sudo rm ${VLC_FILE}
	@sudo rm -R ${SCRATCH_MOUNT}