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
#  Last Modified: 2011/07/18
#
#  Description: Perian ships as a prefPane, which then unpacks its support libs out of
#  zipfiles if it sees they aren't installed. We do this, as well as apply
#  user template prefs that will disable update checks.

include /usr/local/share/luggage/luggage.make

TITLE=Perian
REVERSE_DOMAIN=com.example.corp
PACKAGE_VERSION=1.2.2

PERIAN_DIST_FILE=Perian_1.2.2.dmg
PERIAN_DIST_URL=http://perian.cachefly.net/${PERIAN_DIST_FILE}
PERIAN_PREFPANE=Perian.prefPane
PERIAN_SUPPORT_DIR=Contents/Resources/Components

PAYLOAD=unpack-perian-dist \
		unpack-perian-support \
		pack-Library-PreferencePanes-${PERIAN_PREFPANE} \
		pack-Library-QuickTime-Perian.component \
		pack-Library-QuickTime-AC3MovieImport.component \
		pack-Library-Audio-PlugIns-Components-A52Codec.component \
		pack-user-template-plist-org.perian.Perian.plist \
		pack-user-template-plist-com.cod3r.a52codec.plist \
		cleanup-prefpane

unpack-perian-dist:
	curl -O ${PERIAN_DIST_URL}
	mkdir perian_dist
	hdiutil attach ${PERIAN_DIST_FILE} -mountpoint perian_dist
	${CP} -R perian_dist/${PERIAN_PREFPANE} ./
	hdiutil detach perian_dist
	rm -R perian_dist

unpack-perian-support:
	unzip -o ${PERIAN_PREFPANE}/${PERIAN_SUPPORT_DIR}/Perian.zip -d .
	unzip -o ${PERIAN_PREFPANE}/${PERIAN_SUPPORT_DIR}/CoreAudio/A52Codec.zip -d .
	unzip -o ${PERIAN_PREFPANE}/${PERIAN_SUPPORT_DIR}/QuickTime/AC3MovieImport.zip -d .

l_Library_Audio_PlugIns_Components: l_Library
	@sudo mkdir -p ${WORK_D}/Library/Audio/Plug-Ins/Components
	@sudo chown -R root:admin ${WORK_D}/Library/Audio/Plug-Ins/Components
	@sudo chmod -R 775 ${WORK_D}/Library/Audio/Plug-Ins/Components

pack-Library-Audio-PlugIns-Components-%: % l_Library_Audio_PlugIns_Components
	@sudo ${CP} -R $< ${WORK_D}/Library/Audio/Plug-Ins/Components
	@sudo chown -R root:admin ${WORK_D}/Library/Audio/Plug-Ins/Components/$<
	@sudo chmod -R 775 ${WORK_D}/Library/Audio/Plug-Ins/Components/$<

# the support lib archives we don't need to keep around
cleanup-prefpane:
	@sudo rm -Rf ${WORK_D}/Library/PreferencePanes/${PERIAN_PREFPANE}/Contents/Resources/Components/*