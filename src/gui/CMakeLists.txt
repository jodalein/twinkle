project(twinkle-gui)

include_directories(${CMAKE_CURRENT_BINARY_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

set(twinkle_ui_SRC
	addresscardform.ui
	authenticationform.ui
	buddyform.ui
	deregisterform.ui
	diamondcardprofileform.ui
	dtmfform.ui
	getaddressform.ui
	getprofilenameform.ui
	historyform.ui
	inviteform.ui
	logviewform.ui
	messageform.ui
	mphoneform.ui
	numberconversionform.ui
	redirectform.ui
	selectnicform.ui
	selectprofileform.ui
	selectuserform.ui
	sendfileform.ui
	srvredirectform.ui
	syssettingsform.ui
	termcapform.ui
	transferform.ui
	userprofileform.ui
	wizardform.ui
)

set (twinkle_lang_SRC
	lang/twinkle_cs.ts
	lang/twinkle_de.ts
	lang/twinkle_fr.ts
	lang/twinkle_nl.ts
	lang/twinkle_ru.ts
	lang/twinkle_sv.ts
)

if (WITH_QT4)
qt4_wrap_ui(
	twinkle_UIS
	${twinkle_ui_SRC}
)

qt4_add_resources(twinkle_QRC icons.qrc qml/qml.qrc)

qt4_add_translation(twinkle_LANG
	${twinkle_lang_SRC}
)

set(qt_LIBS Qt4::QtGui Qt4::QtDeclarative)

elseif (WITH_QT5)

qt5_wrap_ui(
	twinkle_UIS
	${twinkle_ui_SRC}
)

qt5_add_resources(twinkle_QRC icons.qrc qml/qml.qrc)

qt5_add_translation(twinkle_LANG
	${twinkle_lang_SRC}
)

set(qt_LIBS Qt5::Widgets Qt5::Quick Qt5::Declarative)
endif (WITH_QT4)

set(CMAKE_AUTOMOC ON)

set(TWINKLE_GUI-SRCS
	mphoneform.cpp
	inviteform.cpp
	getaddressform.cpp
	redirectform.cpp
	termcapform.cpp
	messageform.cpp
	srvredirectform.cpp
	userprofileform.cpp
	transferform.cpp
	syssettingsform.cpp
	historyform.cpp
	selectuserform.cpp
	selectprofileform.cpp
	buddyform.cpp
	diamondcardprofileform.cpp
	addresscardform.cpp
	authenticationform.cpp
	selectnicform.cpp
	sendfileform.cpp
	wizardform.cpp

	address_finder.cpp
	addresstablemodel.cpp
	buddylistview.cpp
	deregisterform.cpp
	dtmfform.cpp
	getprofilenameform.cpp
	gui.cpp
	logviewform.cpp
	main.cpp
	messageformview.cpp
	numberconversionform.cpp
	twinkleapplication.cpp
	yesnodialog.cpp
	textbrowsernoautolink.cpp
	osd.cpp
	incoming_call_popup.cpp

	$<TARGET_OBJECTS:libtwinkle>
	$<TARGET_OBJECTS:libtwinkle-audio>
	$<TARGET_OBJECTS:libtwinkle-gsm>
	$<TARGET_OBJECTS:libtwinkle-audits>
	$<TARGET_OBJECTS:libtwinkle-im>
	$<TARGET_OBJECTS:libtwinkle-mwi>
	$<TARGET_OBJECTS:libtwinkle-parser>
	$<TARGET_OBJECTS:libtwinkle-patterns>
	$<TARGET_OBJECTS:libtwinkle-presence>
	$<TARGET_OBJECTS:libtwinkle-sdp>
	$<TARGET_OBJECTS:libtwinkle-sockets>
	$<TARGET_OBJECTS:libtwinkle-stun>
	$<TARGET_OBJECTS:libtwinkle-threads>
	$<TARGET_OBJECTS:libtwinkle-utils>
	${twinkle_UIS}
	${twinkle_QRC}
	${twinkle_LANG}
)

add_executable(twinkle ${TWINKLE_GUI-SRCS})
target_link_libraries(twinkle -lpthread -lresolv ${LibMagic_LIBRARY} ${LIBXML2_LIBRARIES}
	${Readline_LIBRARY} ${ILBC_LIBRARIES} ${SPEEX_LIBRARIES} ${ZRTPCPP_LIBRARIES}
	${CCRTP_LIBRARIES} ${COMMONCPP_LIBRARIES} ${UCOMMON_LIBRARIES} ${LIBSNDFILE_LIBRARY}
	${Boost_LIBRARIES} ${ALSA_LIBRARY} ${qt_LIBS} ${G729_LIBRARY})

install(TARGETS twinkle DESTINATION bin)
install(FILES ${twinkle_LANG} DESTINATION share/twinkle/lang)
