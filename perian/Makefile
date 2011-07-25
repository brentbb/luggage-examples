#
# Copyright 2009 Joe Block <jpb@ApesSeekingKnowledge.net>
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
#  Author:  Tim S
#  Modified by: Brent B
#  Created: 2011/04/16
#  Last Modified: 2011/07/25
#
#  Description: Perian ships as a prefPane, which then unpacks its support libs out of
#  zipfiles if it sees they aren't installed. We do this, as well as apply
#  user template prefs that will disable update checks.

include /usr/local/share/luggage/luggage.make

TITLE=Perian
REVERSE_DOMAIN=org.perian
PACKAGE_VERSION=1.2.3
SCRATCH_MOUNT=${SCRATCH_D}/dmgmount

PERIAN_DIST_FILE=${TITLE}_${PACKAGE_VERSION}.dmg
PERIAN_DIST_URL=http://perian.cachefly.net/${PERIAN_DIST_FILE}
PERIAN_PREFPANE=Perian.prefPane
PERIAN_SUPPORT_DIR=Contents/Resources/Components
PERIAN_PREF=org.perian.Perian.plist

PAYLOAD=patch-plist \
		pack-Library-PreferencePanes-${PERIAN_PREFPANE} \
		pack-Library-QuickTime-Perian.component \
		pack-Library-QuickTime-AC3MovieImport.component \
		pack-Library-Audio-PlugIns-Components-A52Codec.component \
		pack-Library-Preferences-org.perian.Perian.plist \
		pack-user-template-plist-org.perian.Perian.plist \
		pack-user-template-plist-com.cod3r.a52codec.plist \
		cleanup-prefpane

${PERIAN_DIST_FILE}:
	curl -L -o ${PERIAN_DIST_FILE} ${PERIAN_DIST_URL}

# undmg the prefpane
${PERIAN_PREFPANE}: ${PERIAN_DIST_FILE}
	@sudo mkdir -p ${SCRATCH_MOUNT}
	@sudo hdiutil attach -nobrowse ${PERIAN_DIST_FILE} -mountpoint ${SCRATCH_MOUNT}
	@${DITTO} --noqtn ${SCRATCH_MOUNT}/${PERIAN_PREFPANE} ./${PERIAN_PREFPANE}
	@sudo hdiutil detach ${SCRATCH_MOUNT}
	@sudo rm -R ${SCRATCH_MOUNT}

# unpack the support libs from the prefpane
Perian.component: ${PERIAN_PREFPANE}
	@${DITTO} -k -x ${PERIAN_PREFPANE}/${PERIAN_SUPPORT_DIR}/Perian.zip ./

A52Codec.component: ${PERIAN_PREFPANE}
	@${DITTO} -k -x ${PERIAN_PREFPANE}/${PERIAN_SUPPORT_DIR}/CoreAudio/A52Codec.zip ./

AC3MovieImport.component: ${PERIAN_PREFPANE}
	@${DITTO} -k -x ${PERIAN_PREFPANE}/${PERIAN_SUPPORT_DIR}/QuickTime/AC3MovieImport.zip ./

l_Library_Audio_PlugIns_Components: l_Library
	@sudo mkdir -p ${WORK_D}/Library/Audio/Plug-Ins/Components
	@sudo chown -R root:admin ${WORK_D}/Library/Audio/Plug-Ins/Components
	@sudo chmod -R 775 ${WORK_D}/Library/Audio/Plug-Ins/Components

pack-Library-Audio-PlugIns-Components-%: % l_Library_Audio_PlugIns_Components
	@sudo ${CP} -R $< ${WORK_D}/Library/Audio/Plug-Ins/Components
	@sudo chown -R root:admin ${WORK_D}/Library/Audio/Plug-Ins/Components/$<
	@sudo chmod -R 775 ${WORK_D}/Library/Audio/Plug-Ins/Components/$<

patch-plist: 
	# we need to set the version number in the user pref to disable the nag 
	# for this specific version
	/usr/libexec/PlistBuddy -c "Set :LastInstalledVersion ${PACKAGE_VERSION}" ${PERIAN_PREF}

# the support lib archives we don't need to keep around
cleanup-prefpane:
	@sudo rm -Rf ${WORK_D}/Library/PreferencePanes/${PERIAN_PREFPANE}/${PERIAN_SUPPORT_DIR}/*

# remove our temporary/unpacked files
distclean: clean
	@rm -Rf ${PERIAN_DIST_FILE} ${PERIAN_PREFPANE} Perian.component A52Codec.component AC3MovieImport.component