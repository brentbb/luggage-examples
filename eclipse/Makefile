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

# Eclipse Classic SDK 32-bit
# - update the URL as necessary

include /usr/local/share/luggage/luggage.make

TITLE=Eclipse-Classic-SDK-32bit
REVERSE_DOMAIN=ca.concordia.cda
PACKAGE_VERSION=3.6.2

PAYLOAD=unpack-eclipse

ECLIPSE_DIST_FILE=eclipse-SDK-3.6.2-macosx-cocoa.tar.gz
ECLIPSE_DIST_URL=http://mirror.cc.vt.edu/pub/eclipse/eclipse/downloads/drops/R-3.6.2-201102101200/${ECLIPSE_DIST_FILE}

unpack-eclipse: l_Applications
	curl ${ECLIPSE_DIST_URL} -O
	@sudo ${TAR} xzf ${ECLIPSE_DIST_FILE}
	@sudo ${CP} -R eclipse ${WORK_D}/Applications