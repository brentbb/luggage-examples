#
#   Copyright 2009 Joe Block <jpb@ApesSeekingKnowledge.net>
#
#   Licensed under the Apache License, Version 2.0 (the "License");
#   you may not use this file except in compliance with the License.
#   You may obtain a copy of the License at
#
#       http://www.apache.org/licenses/LICENSE-2.0
#
#   Unless required by applicable law or agreed to in writing, software
#   distributed under the License is distributed on an "AS IS" BASIS,
#   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#   See the License for the specific language governing permissions and
#   limitations under the License.
#
#  Author:  Tim S
#  Created: 2011/04/19
#  Last Modified: 2011/06/09
#
#  Description:  Download and package the specified version of VLC (PowerPC or Intel), and add user template plist for update-check suppression.

include /usr/local/share/luggage/luggage.make

TITLE=VLC
REVERSE_DOMAIN=org.videolan
PACKAGE_VERSION=1.1.10
# run make with ARCH=PowerPC to build the PPC version
ARCH=i386
PAYLOAD=undmg-applications-vlc \
		pack-user-template-plist-org.videolan.vlc.plist

VLC_FILE=vlc-${PACKAGE_VERSION}.dmg
ifeq (${ARCH},PowerPC)
	VLC_FILE=vlc-${PACKAGE_VERSION}-powerpc.dmg
	TITLE=VLC-PowerPC
endif

VLC_URL=http://downloads.sourceforge.net/project/vlc/${PACKAGE_VERSION}/macosx/${VLC_FILE}
SCRATCH_MOUNT=${SCRATCH_D}/dmgmount

undmg-applications-vlc:	l_Applications
	curl -L -O ${VLC_URL}
	@sudo mkdir -p ${SCRATCH_MOUNT}
	@sudo hdiutil attach ${VLC_FILE} -mountpoint ${SCRATCH_MOUNT}
	@sudo ${DITTO} --noqtn ${SCRATCH_MOUNT}/VLC.app ${WORK_D}/Applications/VLC.app
	@sudo chown -R root:admin ${WORK_D}/Applications/VLC.app
	@sudo hdiutil detach ${SCRATCH_MOUNT}
	# since the downloaded file has the same name as what we might be building...
	@sudo rm ${VLC_FILE}
	@sudo rm -R ${SCRATCH_MOUNT}