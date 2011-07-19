#
#   Copyright 2011 Brent B <brent dot bb plus luggage at gmail dot com>
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
#
#  Author:  Brent B
#  Created: 2011/07/18
#  Last Modified: 2011/07/18
#
#  Description: Download the specified version of Firefox and repack it.
#  This is just a vanilla Firefox, please see CCK for customizations.

include /usr/local/share/luggage/luggage.make
SCRATCH_MOUNT=${SCRATCH_D}/dmgmount

TITLE=Firefox
REVERSE_DOMAIN=com.mozilla
PACKAGE_VERSION=5.0.1
PACKAGE_MAJOR_VERSION=5
PACKAGE_MINOR_VERSION=0

FF_DIST_FILE=${TITLE}_${PACKAGE_VERSION}.dmg

${FF_DIST_FILE}:
	#-L follow redirects -G make this a GET -d get parameters...
	/usr/bin/curl -L -G -d product=firefox-${PACKAGE_VERSION} -d os=osx -d lang=en-US http://download.mozilla.org/  -o ${FF_DIST_FILE}

${TITLE}.app: ${FF_DIST_FILE}
	@sudo mkdir -p ${SCRATCH_MOUNT}
	@sudo hdiutil attach -nobrowse ${FF_DIST_FILE} -mountpoint ${SCRATCH_MOUNT}
	@sudo ${DITTO} ${SCRATCH_MOUNT}/${TITLE}.app ./${TITLE}.app
	@sudo hdiutil detach ${SCRATCH_MOUNT}
	@sudo rm -R ${SCRATCH_MOUNT}

pack-applications-%: % l_Applications
	@sudo ${DITTO} --noqtn $< ${WORK_D}/Applications/$<
	@sudo chown -R root:admin ${WORK_D}/Applications/$<

distclean: clean
	@sudo rm -Rf ${FF_DIST_FILE} ${TITLE}.app

PAYLOAD=pack-applications-Firefox.app
