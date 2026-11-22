# Haxball-1.0
(async () => {
    "use strict";

    const SOURCE =
        "https://raw.githubusercontent.com/VixelDevelopment/HaxballMobile/main/old.min.js";

    // RED NEON MOBILE CONTROLS
    const controlsCSS = `
    #joystick,#kick {
        z-index:99999 !important;
        bottom:CONTROLS_MARGINvw;
        touch-action:none !important;
        pointer-events:auto !important;
    }

    .neo {
        opacity:CONTROLS_OPACITY;
        background:#080808ee;
        border:2px solid #ff1744;
        box-shadow:
            0 0 5px #ff1744,
            0 0 12px #ff1744,
            inset 0 0 8px #ff174455;
        color:#fff;
        font-weight:bold;
        font-size:1.5rem;
    }

    .sizer {
        width:CONTROLS_WIDTH%;
        aspect-ratio:1/1;
    }

    #joystick {
        left:CONTROLS_MARGIN%;
        overflow:visible;
        touch-action:none !important;
        pointer-events:auto !important;
    }

    #thumb {
        width:40%;
        height:40%;
        background:#ff1744;
        border:2px solid #ff8a9b;
        box-shadow:
            0 0 8px #ff1744,
            0 0 18px #ff1744,
            0 0 30px #ff174488;
        pointer-events:none !important;
    }

    #kick {
        right:CONTROLS_MARGIN%;
        background:#a00020ee;
        border:2px solid #ff1744;
        box-shadow:
            0 0 8px #ff1744,
            0 0 18px #ff1744,
            inset 0 0 10px #ff174455;
    }

    #kick svg {
        fill:#fff;
        filter:drop-shadow(0 0 5px #ff1744);
    }

    button.neo:active {
        opacity:KICK_OPACITY;
        background:#ff1744;
        box-shadow:0 0 12px #ff1744,0 0 30px #ff1744;
    }
    `;

    // BLACK RED NEON THEME
    const themeCSS = `
    body {
        background:#050505 !important;
        color:#fff !important;
    }

    .dialog,
    .roomlist-view,
    .room-view,
    .settings-view,
    .create-room-view,
    .choose-nickname-view {
        background:#090909 !important;
        color:#fff !important;
        border:1px solid #ff1744 !important;
        box-shadow:
            0 0 8px #ff1744,
            0 0 20px #ff174455,
            inset 0 0 12px #ff174422 !important;
        animation:revengeNeon 2s ease-in-out infinite;
    }

    button {
        background:#0b0b0b !important;
        color:#fff !important;
        border:1px solid #ff1744 !important;
        box-shadow:
            0 0 5px #ff1744,
            inset 0 0 8px #ff174422 !important;
        text-shadow:0 0 6px #ff304f;
    }

    button:active {
        background:#a00020 !important;
        box-shadow:0 0 12px #ff1744,0 0 25px #ff1744 !important;
    }

    input,select,textarea {
        background:#080808 !important;
        color:#fff !important;
        border:1px solid #ff1744 !important;
        box-shadow:0 0 7px #ff174455 !important;
    }

    h1,h2,h3 {
        color:#ff1744 !important;
        text-shadow:
            0 0 5px #ff1744,
            0 0 12px #ff1744,
            0 0 24px #ff174488;
    }

    a {
        color:#ff526d !important;
        text-shadow:0 0 6px #ff1744;
    }

    [data-hook=leave-btn] {
        background:#a00020 !important;
        box-shadow:0 0 12px #ff1744 !important;
    }

    .input-options {
        background:#050505 !important;
    }

    @keyframes revengeNeon {
        0%,100% {
            box-shadow:0 0 5px #ff1744,0 0 12px #ff1744;
        }
        50% {
            box-shadow:
                0 0 10px #ff1744,
                0 0 25px #ff1744,
                0 0 40px #ff174488;
        }
    }
    `;

    function replaceRequired(source, pattern, replacement, label) {
        const result = source.replace(pattern, replacement);
        if (result === source) {
            throw new Error("Patch failed: " + label);
        }
        return result;
    }

    // VIETNAMESE TRANSLATION
    const vietnameseInjection = `
    (() => {
        const doc = gameFrame.document;

        const translations = {
            "Play":"Chơi",
            "Create Room":"Tạo phòng",
            "Create room":"Tạo phòng",
            "Room List":"Danh sách phòng",
            "Room list":"Danh sách phòng",
            "Settings":"Cài đặt",
            "Nickname":"Biệt danh",
            "Password":"Mật khẩu",
            "Join":"Tham gia",
            "Join Room":"Vào phòng",
            "Leave":"Rời phòng",
            "Spectators":"Khán giả",
            "Players":"Người chơi",
            "Player":"Người chơi",
            "About":"Giới thiệu",
            "About us":"Giới thiệu",
            "Close":"Đóng",
            "Back":"Quay lại",
            "Cancel":"Hủy",
            "Save":"Lưu",
            "Search":"Tìm kiếm",
            "Refresh":"Làm mới",
            "Region":"Khu vực",
            "Country":"Quốc gia",
            "Name":"Tên",
            "Room name":"Tên phòng",
            "Max players":"Số người tối đa",
            "Public":"Công khai",
            "Private":"Riêng tư",
            "Start":"Bắt đầu",
            "Stop":"Dừng",
            "Chat":"Trò chuyện",
            "Send":"Gửi",
            "Create":"Tạo",
            "Change":"Thay đổi",
            "Apply":"Áp dụng",
            "Reset":"Đặt lại",
            "Yes":"Có",
            "No":"Không",
            "OK":"Đồng ý",
            "Loading":"Đang tải",
            "Connecting":"Đang kết nối",
            "Disconnected":"Đã ngắt kết nối",
            "Game settings":"Cài đặt trận đấu",
            "Room settings":"Cài đặt phòng",
            "Player settings":"Cài đặt người chơi",
            "Team":"Đội",
            "Red":"Đỏ",
            "Blue":"Xanh",
            "Auto":"Tự động",
            "Random":"Ngẫu nhiên",
            "None":"Không",
            "Choose nickname":"Chọn biệt danh",
            "Enter password":"Nhập mật khẩu",
            "Room is full":"Phòng đã đầy"};

        function translateNode(node) {
            if (node.nodeType === 3) {
                const original = node.nodeValue.trim();
                if (translations[original]) {
                    node.nodeValue = node.nodeValue.replace(
                        original,
                        translations[original]
                    );
                }
                return;
            }

            if (node.nodeType !== 1) return;
            if (/^(SCRIPT|STYLE|TEXTAREA)$/i.test(node.tagName)) return;

            ["placeholder","title","aria-label"].forEach(attr => {
                const value = node.getAttribute(attr);
                if (value && translations[value]) {
                    node.setAttribute(attr, translations[value]);
                }
            });

            Array.from(node.childNodes).forEach(translateNode);
        }

        function startTranslation() {
            if (!doc.body) {
                const observer = new MutationObserver(() => {
                    if (doc.body) {
                        observer.disconnect();
                        startTranslation();
                    }
                });

                observer.observe(doc.documentElement, {
                    childList:true,
                    subtree:true
                });
                return;
            }

            translateNode(doc.body);

            const observer = new MutationObserver(mutations => {
                for (const mutation of mutations) {
                    if (mutation.type === "characterData") {
                        translateNode(mutation.target);
                    }
                    mutation.addedNodes.forEach(translateNode);
                }
            });

            observer.observe(doc.body, {
                childList:true,
                subtree:true,
                characterData:true
            });

            console.log("[HaxBall] Vietnamese enabled");
        }

        startTranslation();
    })();
    `;

    try {
        console.log("[REVENGE CLIENT] Loading...");

        const response = await fetch(SOURCE, {
            cache:"no-store"
        });

        if (!response.ok) {
            throw new Error("Cannot load Vixel source");
        }

        let code = await response.text();

        // MOBILE CONTROLS CSS
        code = replaceRequired(
            code,
            /const constrolsStyleBase\s*=\s*"[^"]*";/,
            "const constrolsStyleBase = " +
                JSON.stringify(controlsCSS) + ";",
            "Controls CSS"
        );

        // JOYSTICK VARIABLES
        code = replaceRequired(
            code,
            "let kickButton;",
            "let kickButton;\nlet thumb;\nlet isTouching = false;",
            "Joystick variables"
        );

        // JOYSTICK THUMB
        code = replaceRequired(
            code,
            `joystick.innerHTML = '<div id="thumb" class="rounded" float></div>';`,
            `joystick.innerHTML = '<div id="thumb" class="rounded" float></div>';
    thumb = joystick.querySelector("#thumb");`,
            "Thumb assignment"
        );

        // TOUCH START
        code = replaceRequired(
            code,
            /function handleTouchStart\(e\)\s*\{[\s\S]*?\n\}/,
            `function handleTouchStart(e) {
    if (!e.touches || !e.touches.length) return;
    e.preventDefault();
    isTouching = true;
    updateJoystick(e.touches[0]);
}`,
            "Touch start"
        );

        // TOUCH MOVE
        code = replaceRequired(
            code,
            /function handleTouchMove\(e\)\s*\{[\s\S]*?\n\}/,
            `function handleTouchMove(e) {
    if (!isTouching || !e.touches || !e.touches.length) return;
    e.preventDefault();
    updateJoystick(e.touches[0]);
}`,
            "Touch move"
        );

        // TOUCH END
        code = replaceRequired(
            code,
            /function handleTouchEnd\(\)\s*\{[\s\S]*?\n\}/,
            `function handleTouchEnd(e) {
    if (e && e.preventDefault) e.preventDefault();
    isTouching = false;
    resetJoystick();
}`,
            "Touch end"
        );

        // TOUCH LISTENERS
        code = replaceRequired(
            code,
            `joystick.addEventListener('touchstart', handleTouchStart);
    joystick.addEventListener('touchmove', handleTouchMove);
    joystick.addEventListener('touchend', handleTouchEnd);`,
            `joystick.addEventListener('touchstart', handleTouchStart, { passive:false });
    joystick.addEventListener('touchmove', handleTouchMove, { passive:false });
    joystick.addEventListener('touchend', handleTouchEnd, { passive:false });
    joystick.addEventListener('touchcancel', handleTouchEnd, { passive:false });`,
            "Touch listeners"
        );

        // BLACK RED BRANDING
        code = code.replaceAll("#1a2125", "#050505");
        code = code.replaceAll("#c13535", "#ff1744");
        code = code.replaceAll("Vixel Dev", "REVENGE CLIENT");
        code = code.replaceAll("About us", "REVENGE CLIENT");

        const aboutHTML =
            '<div class="dialog basic-dialog" style="max-width:85%;">' +
            '<h1>REVENGE CLIENT</h1>' +
            '<p>Black × Red Neon Mobile Edition.</p>' +
            '<p>Vietnamese Interface.</p>' +
            '<p>Original game by Mario Carbajal (@basro).</p>' +
            '<div class="buttons"><button data-hook="closeabout">Close</button></div>' +
            '</div>';

        code = replaceRequired(
            code,
            /aboutHandler\.innerHTML\s*=\s*'[\s\S]*?';/,
            "aboutHandler.innerHTML = " + JSON.stringify(aboutHTML) + ";",
            "About window"
        );

        // THEME + TRANSLATION
        const themeInjection = `
            const revengeTheme = gameFrame.document.createElement("style");
            revengeTheme.textContent = ${JSON.stringify(themeCSS)};
            gameFrame.document.head.appendChild(revengeTheme);
        `;

        code = replaceRequired(
            code,
            "setupCountryFilter();",
            "setupCountryFilter();\n" +
                themeInjection + "\n" +
                vietnameseInjection,
            "Theme and Vietnamese injection"
        );

        // START CLIENT
        eval(code);

        // MOBILE LAYOUT FIX
        const revengeLayout = document.createElement("style");

        revengeLayout.textContent = `
            html, body {
                width:100% !important;
                min-width:0 !important;
                height:100% !important;
                min-height:100% !important;
                margin:0 !important;
                padding:0 !important;
                background:#050505 !important;
            }

            .gameframe {
                display:block !important;
                width:100% !important;
                height:100vh !important;
                height:100dvh !important;
                min-height:100vh !important;
                min-height:100dvh !important;
                max-height:none !important;
                margin:0 !important;
                padding:0 !important;
                border:0 !important;
            }

            .gameframe iframe {
                display:block !important;
                width:100% !important;
                height:100% !important;
                min-height:100% !important;
                border:0 !important;
            }
        `;

        document.head.appendChild(revengeLayout);

        function fixGameFrame() {
            const frame = document.querySelector(".gameframe");

            if (!frame) return false;

            frame.style.setProperty("width","100%","important");
            frame.style.setProperty("height","100dvh","important");
            frame.style.setProperty("min-height","100dvh","important");
            frame.style.setProperty("max-height","none","important");

            if (frame.tagName === "IFRAME") {
                frame.style.setProperty("display","block","important");
            }

            const innerFrame = frame.querySelector("iframe");

            if (innerFrame) {
                innerFrame.style.setProperty("width","100%","important");
                innerFrame.style.setProperty("height","100%","important");
                innerFrame.style.setProperty("border","0","important");
            }

            return true;
        }

        if (!fixGameFrame()) {
            const layoutObserver = new MutationObserver(() => {
                if (fixGameFrame()) {
                    layoutObserver.disconnect();
                }
            });

            layoutObserver.observe(document.documentElement, {
                childList:true,
                subtree:true
            });
        }

        console.log(
            "%c REVENGE CLIENT NEON LOADED ",
            "background:#ff1744;color:white;font-weight:bold;padding:8px"
        );

    } catch (error) {
        console.error("[REVENGE CLIENT ERROR]", error);
    }
})();
