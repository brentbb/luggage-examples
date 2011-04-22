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
#  Created: 2011/04/21
#  Last Modified: 2011/04/21
#
#  Description:  Download and package the specified version of SuperCollider (64-bit/32-bit universal version only) and the distributed sc3-plugins.

include /usr/local/share/luggage/luggage.make

TITLE=SuperCollider-WithPlugins
REVERSE_DOMAIN=com.example.corp
PACKAGE_VERSION=3.4.3

PAYLOAD=undmg-sc \
		unpack-sc3-plugins \
		pack-sc3-plugins

SC_APPSUPPORT_DIR=${WORK_D}/Library/Application\ Support/SuperCollider
SCRATCH_MOUNT=${SCRATCH_D}/dmgmount

SC_FILE=SuperCollider-${PACKAGE_VERSION}_32_64.dmg
SC_URL=http://iweb.dl.sourceforge.net/project/supercollider/Mac%20OS%20X/${PACKAGE_VERSION}/${SC_FILE}

PLUGINS_FILE=sc3-plugins_32_64bit.tar.gz
PLUGINS_URL=http://iweb.dl.sourceforge.net/project/sc3-plugins/SC%20${PACKAGE_VERSION}%20snapshot/Mac%20OS/${PLUGINS_FILE}

l_Library_Application_Support_SuperCollider: l_Library_Application_Support
	@sudo mkdir ${WORK_D}/Library/Application\ Support/SuperCollider
	@sudo chown root:admin ${WORK_D}/Library/Application\ Support/SuperCollider
	@sudo chmod 775 ${WORK_D}/Library/Application\ Support/SuperCollider

l_Library_Application_Support_SuperCollider_Extensions: l_Library_Application_Support_SuperCollider
	@sudo mkdir ${WORK_D}/Library/Application\ Support/SuperCollider/Extensions
	@sudo chown root:admin ${WORK_D}/Library/Application\ Support/SuperCollider/Extensions
	@sudo chmod 775 ${WORK_D}/Library/Application\ Support/SuperCollider/Extensions

undmg-sc: l_Applications
# download SC
	curl -O ${SC_URL}
# set up mount
	@sudo mkdir ${SCRATCH_MOUNT}
	@sudo hdiutil attach ${SC_FILE} -mountpoint ${SCRATCH_MOUNT}
# SC app folder
	@sudo ${CP} -R ${SCRATCH_MOUNT}/SuperCollider ${WORK_D}/Applications/
	@sudo chown -R root:admin ${WORK_D}/Applications/SuperCollider
# unmount
	@sudo hdiutil detach ${SCRATCH_MOUNT}

unpack-sc3-plugins:
# download sc3-plugins
	curl -O ${PLUGINS_URL}
# unpack
	@sudo ${TAR} xzf ${PLUGINS_FILE}

pack-sc3-plugins: l_Library_Application_Support_SuperCollider l_Library_Application_Support_SuperCollider_Extensions
	@sudo ${CP} -R build/* ${WORK_D}/Library/Application\ Support/SuperCollider/Extensions/
	@sudo rm -R build
	@sudo chown -R root:admin ${SC_APPSUPPORT_DIR}/Extensions/*
	@sudo chmod -R 755 ${SC_APPSUPPORT_DIR}/Extensions/*