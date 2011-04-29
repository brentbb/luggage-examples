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
#
#  Author:  Tim S
#  Created: 2011/04/23
#  Last Modified: 2011/04/21
#
#  Description: Download the specified version of Cyberduck, pack it, set
#  the appropriate version number to disable the reminder, and drop in
#  a template bookmark for an organization's deployment.

include /usr/local/share/luggage/luggage.make

TITLE=Cyberduck
REVERSE_DOMAIN=com.example.corp
PACKAGE_VERSION=4.0.2

CD_FILE=Cyberduck-${PACKAGE_VERSION}.zip
CD_URL=http://cyberduck.ch/${CD_FILE}
CD_PREF=ch.sudo.cyberduck.plist
CD_BOOKMARK=example_bookmark.duck

PAYLOAD=\
		unpack-cd \
		patch-plist \
		pack-cd \
		pack-user-template-plist-${CD_PREF} \
		pack-user-template-appsupport-cd-bookmarks

unpack-cd: l_Applications
	# we need -L to let curl redirect to the CDN
	curl -L ${CD_URL} -o ${CD_FILE}

patch-plist:
	# we need to set the version number in the user pref to disable the nag 
	# for this specific version
	/usr/libexec/PlistBuddy -c "Set :donate.reminder ${PACKAGE_VERSION}" ${CD_PREF}

pack-cd: l_Applications
	# ditto out to Applications
	@sudo ${DITTO} -x -k --noqtn ${CD_FILE} ${WORK_D}/Applications/

pack-user-template-appsupport-cd-bookmarks: l_System_Library_User_Template_Application_Support_Cyberduck_Bookmarks
	# each .duck file is a bookmark - login user and UUID keys can be left
	# empty, login user will use the logged-in user's shortname and UUID will
	# self-generate and rename the .duck file in the user's profile
	@sudo ${CP} ${CD_BOOKMARK} ${USER_TEMPLATE_APPLICATION_SUPPORT}/Cyberduck/Bookmarks

l_System_Library_User_Template_Application_Support_Cyberduck_Bookmarks: l_System_Library_User_Template_Application_Support
	@sudo mkdir -p ${USER_TEMPLATE_APPLICATION_SUPPORT}/Cyberduck/Bookmarks
	@sudo chown root:wheel ${USER_TEMPLATE_APPLICATION_SUPPORT}/Cyberduck/Bookmarks
	@sudo chmod -R 700 ${USER_TEMPLATE_APPLICATION_SUPPORT}/Cyberduck/Bookmarks