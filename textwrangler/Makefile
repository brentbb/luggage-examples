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
#  Created: 2011/04/30
#  Last Modified: 2011/04/30
#
#  Description: Download the specified version of TextWrangler, pack it, set
#  the appropriate version number to disable the update prompt, and drop in
#  a template preference file and CLI tools to disable the first run prompts.

include /usr/local/share/luggage/luggage.make

TITLE=TextWrangler
REVERSE_DOMAIN=com.barebones
PACKAGE_VERSION=3.5.3
PACKAGE_MAJOR_VERSION=3
PACKAGE_MINOR_VERSION=5

TW_FILE=${TITLE}_${PACKAGE_VERSION}.dmg
TW_URL=http://pine.barebones.com/files/${TW_FILE}
SCRATCH_MOUNT=${SCRATCH_D}/dmgmount

TextWrangler.app:
	curl -O ${TW_URL}
	@sudo mkdir ${SCRATCH_MOUNT}
	@sudo hdiutil attach -nobrowse ${TW_FILE} -mountpoint ${SCRATCH_MOUNT}
	@sudo ${DITTO} ${SCRATCH_MOUNT}/${TITLE}.app ${TITLE}.app
	@sudo hdiutil detach ${SCRATCH_MOUNT}
	@rm ${TW_FILE}
	@sudo rm -R ${SCRATCH_MOUNT}

#Copy out the CLI helpers, then use the built-in pack-usr-bin rules to place them
edit: ${TITLE}.app
	@${DITTO} ${TITLE}.app/Contents/MacOS/edit edit

twdiff: ${TITLE}.app
	@${DITTO} ${TITLE}.app/Contents/MacOS/twdiff twdiff

twfind: ${TITLE}.app
	@${DITTO} ${TITLE}.app/Contents/MacOS/twfind twfind

pack-applications-%: % l_Applications
	@sudo ${DITTO} --noqtn $< ${WORK_D}/Applications/$<
	@sudo chown -R root:admin ${WORK_D}/Applications/$<

# Included plist disabled first-run popups, keep the version updated
patch-plist: com.barebones.textwrangler.plist
	@/usr/libexec/PlistBuddy -c "Set :LastAppVersion ${PACKAGE_VERSION}" com.barebones.textwrangler.plist

clean-local:
	@rm -Rf edit twdiff twfind TextWrangler.app

#Pack the main TextWrangler.app, install the commandline tools, and install a default preference into the User Template to reduce nagging
#Optional, clean up
PAYLOAD=pack-applications-TextWrangler.app \
patch-plist \
pack-usr-bin-edit \
pack-usr-bin-twdiff \
pack-usr-bin-twfind \
pack-user-template-plist-com.barebones.textwrangler.plist \
clean-local
