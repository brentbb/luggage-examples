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
# MPlayer OSX Extended for lab use, where all users are created from
# User Template
#
# - Packages up MPlayer-OSX-Extended dl'ed from the source URL
# - applies prefs to:
#    - suppress updates
#    - enable the multi-threaded mplayer binary
#    - choose a default font for subs (with none selected, subs won't
#      be available)
# - set fontconfig within .app to generate caches in /Users/Shared
#   instead of the user's home

include /usr/local/share/luggage/luggage.make

TITLE=MPlayerOSXExtended-Custom
REVERSE_DOMAIN=com.example.corp
PACKAGE_VERSION=14.20110109

PAYLOAD=\
		unpack-mp-osx-ext \
		unpack-mp-osx-fontconfig-redirect \
		pack-user-template-plist-hu.mplayerhq.mplayerosx.extended.plist

MPOSXEXT_DIST_FILE=MPlayer-OSX-Extended_rev14.zip
MPOSXEXT_DIST_URL=http://mplayerosxext.googlecode.com/files/${MPOSXEXT_DIST_FILE}

# optionally use the bleeding-edge mplayer builds available at
# http://mplayerosx-builds.googlecode.com
# - add unpack-mp-git to the PAYLOAD to use this
#
# - since it's missing DVD support, not using it at the moment
# - would install to the user template application support folder where
#   mplayer-osx-extended will automatically look for it
# - if it's in use, MPESelectedBinary in pref plist should be set to point to it
#   instead of officialsvnwithmt

MPGIT_DIST_FILE=mplayer-git-2011-01-09.zip
MPGIT_DIST_URL=http://mplayerosx-builds.googlecode.com/files/${MPGIT_DIST_FILE}
MPGIT_MPBINARIES=mplayer-git.mpBinaries

unpack-mp-osx-ext: l_Applications
	curl ${MPOSXEXT_DIST_URL} -O
	@sudo ${UNZIP} -o ${MPOSXEXT_DIST_FILE} -d ${WORK_D}/Applications/

unpack-mp-osx-fontconfig-redirect: l_Users_Shared
#	redirect the .fontconfig cache to /Users/Shared
	sed -i .bak 's/\<cachedir\>\~\/\.fontconfig\<\/cachedir\>/\<cachedir\>\/Users\/Shared\/\.fontconfig\<\/cachedir\>/g' ${WORK_D}/Applications/MPlayer\ OSX\ Extended.app/Contents/Resources/fonts/fonts.conf
#	Set up the Shared .fontconfig area with 777 permissions, ensuring any user can write to them when the cache needs to be (re-)generated
	@sudo mkdir ${WORK_D}/Users/Shared/.fontconfig
	@sudo chown root:wheel ${WORK_D}/Users/Shared/.fontconfig
	@sudo chmod 777 ${WORK_D}/Users/Shared/.fontconfig

unpack-mp-git: l_System_Library_User_Template_Library_Application_Support_Mplayer_OSX_Extended_Binaries
	curl ${MPGIT_DIST_URL} -O
	@sudo ${UNZIP} -o ${MPGIT_DIST_FILE} -d ${USER_TEMPLATE_APPLICATION_SUPPORT}/MPlayer\ OSX\ Extended/Binaries

# only used for unpack-mp-git which is not in use ATM
l_System_Library_User_Template_Library_Application_Support_Mplayer_OSX_Extended_Binaries: l_System_Library_User_Template_Library
	@sudo mkdir -p ${USER_TEMPLATE_APPLICATION_SUPPORT}/MPlayer\ OSX\ Extended/Binaries
	@sudo chown root:wheel ${USER_TEMPLATE_APPLICATION_SUPPORT}/MPlayer\ OSX\ Extended/Binaries
	@sudo chmod 700 ${USER_TEMPLATE_APPLICATION_SUPPORT}/MPlayer\ OSX\ Extended/Binaries