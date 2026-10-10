print('*****************************')
print('*****这是知到的自动刷课脚本******')
print('*****************************')
print('在初次点击课堂听课时，会有个人诚信声明，请自行点击确认，为自己的行为负责;若没有，不必理会此条提醒。')
print('在初次点击课堂听课时，会有个人诚信声明，请自行点击确认，为自己的行为负责;若没有，不必理会此条提醒。')
print('在初次点击课堂听课时，会有个人诚信声明，请自行点击确认，为自己的行为负责;若没有，不必理会此条提醒。')
input("\n点击回车键，确认继续！")
from selenium import webdriver
from selenium.webdriver.edge.options import Options
from selenium.webdriver.edge.service import Service
from selenium.webdriver.common.by import By
from selenium.webdriver.common.action_chains import ActionChains
from selenium.common import TimeoutException, NoSuchElementException
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as ec
import threading
import time
import sys

edge_option = Options()
edge_option.add_argument("--no-sandbox")
edge_option.add_experimental_option("detach", True)
edge_option.add_argument("--disable-blink-features=AutomationControlled")
edge_option.add_experimental_option("excludeSwitches", ['enable-automation'])
edge_option.add_argument('--log-level=3')
edge_option.add_argument('--disable-logging')
edge_option.add_experimental_option('excludeSwitches', ['enable-logging'])

open_edge = webdriver.Edge(service=Service('msedgedriver.exe'), options=edge_option)
open_edge.minimize_window()
open_edge.get('https://onlineweb.zhihuishu.com/onlinestuh5')

print('\n*****请选择登录方式*****')
print('使用提醒:')
print('若是账号密码登录，安全验证请自行完成!!!\n其他之外的东西不要动!!!')
print('[0]账号密码登录\n[1]微信扫码登录\n[2]知到扫码登录\n')
login_num = int(input('操作选择:'))
try:
    if login_num == 0:
        print('\n账号密码登录')
        print('记得自行完成安全验证')
        id = int(input('请输入手机号:'))
        psd = input('请输入密码:')
        open_edge.maximize_window()
        time.sleep(1)
        open_edge.find_element(By.XPATH, '//*[@id="lUsername"]').send_keys(f'{id}')
        time.sleep(1)
        open_edge.find_element(By.XPATH, '//*[@id="lPassword"]').send_keys(f'{psd}')
        time.sleep(1)
        open_edge.find_element(By.XPATH, '//*[@id="f_sign_up"]/div[1]/span').click()
        open_edge.implicitly_wait(60)
        if (open_edge.find_element(By.XPATH, '//*[@id="form-ipt-error-l-username"]').text == '手机号或密码错误'):
            open_edge.minimize_window()
            print('手机号或密码错误')
            exit(0)
        else:
            open_edge.find_element(By.XPATH, '//*[@id="dif_v1"]/div/div')  # 个人首页
    elif login_num == 1:
        print('\n微信扫码登录\n')
        open_edge.maximize_window()
        try:
            open_edge.implicitly_wait(120)
            open_edge.find_element(By.XPATH, '//*[@id="headerMain"]/ul/li[4]/a').click()
        except:
            print('登录超时')
    elif login_num == 2:
        print('\n知到扫码登录\n')
        open_edge.maximize_window()
        open_edge.find_element(By.XPATH, '/html/body/div[9]/div[1]/div[2]').click()
        open_edge.implicitly_wait(120)
        try:
            open_edge.find_element(By.XPATH, '//*[@id="headerMain"]/ul/li[4]/a').click()
        except:
            pass
        finally:
            open_edge.find_element(By.XPATH, '//*[@id="dif_v1"]/div/div/div[1]/a/img')
except:
    print('\n数字不符合要求！！！请输入[]内的数字！！！\n')
    exit(0)

# 课程开始
open_edge.minimize_window()
time.sleep(1)
print('\n正在扫描课程与进度...')


# 扫描课程与进度，进行选择
def course():
    time.sleep(1)
    all_course = open_edge.find_elements(By.XPATH, '//*[@id="sharingClassed"]/div[2]/ul/div/dl/dt/div[1]/div[1]')  # 所有课程
    all_progress = open_edge.find_elements(By.XPATH, '//*[@id="sharingClassed"]/div[2]/ul/div/dl/dt/div[1]/div[3]/div[2]/span[2]')  # 所有进度
    if len(all_course) == 0:
        print('没有扫描到课程，请确认登录成功并进入学生首页后重新运行。')
        try:
            open_edge.quit()
        except:
            pass
        exit(0)
    a_time = []
    for i in range(0, len(all_course)):
        a_time.append(i)  # 等待元素加载
        progress_text = all_progress[i].text if i < len(all_progress) else '未知'
        print(f'[{i}]{all_course[i].text}--{progress_text}')  # 0开始
    while True:
        user_input = input('请输入[]内的数字,选择将要学习的课程:').strip()
        if user_input.isdigit():
            course_num = int(user_input)
            if 0 <= course_num <= a_time[-1]:
                break
        print("数字不符合要求！！！请输入[]内的数字！！！")
    # 点击课堂
    open_edge.find_element(By.XPATH, f'//*[@id="sharingClassed"]/div[2]/ul[{course_num+1}]/div/dl/dt/div[1]/div[1]').click()


time.sleep(1)
course()
open_edge.maximize_window()

open_edge.implicitly_wait(3)
time.sleep(1)
print('\n已开始自动学习,代码执行中...\n\n除了安全验证以外，请勿打断代码执行!!!')
try:  # 广告
    open_edge.implicitly_wait(2)
    open_edge.find_element(By.XPATH, '//*[@id="app"]/div/div[9]/div/div[2]/div/div[3]/div[1]').click()
except:
    pass

# open_edge.minimize_window()
m = WebDriverWait(open_edge, 2, 0.5)
wait = WebDriverWait(open_edge, 7200, 0.5)


# 操作暂停、关闭声音
class Movement:
    @staticmethod
    def play():
        try:
            q = m.until(ec.element_to_be_clickable((By.XPATH, '//*[@id="playButton"]')))
            q.click()  # 播放键
        except Exception:
            # 新版播放器兜底：直接让 HTML5 video 播放
            open_edge.execute_script(
                "const v=document.querySelector('video'); if(v){v.muted=true; v.play().catch(()=>{});}"
            )

    @staticmethod
    def next():
        w = m.until(ec.element_to_be_clickable((By.XPATH, '//*[@id="nextBtn"]')))
        w.click()

    @staticmethod
    def close_voice():
        try:
            e = m.until(ec.element_to_be_clickable((By.XPATH, '//*[@id="vjs_container"]/div[10]/div[7]/div[1]')))
            e.click()  # 关闭音量
        except Exception:
            # 新版播放器直接静音 HTML5 video
            open_edge.execute_script("const v=document.querySelector('video'); if(v) v.muted = true;")


event1 = threading.Event()  # 主
event2 = threading.Event()  # 子
reset_event = threading.Event()  # 命令行按回车触发重置
last_alert_time = 0
security_warned = False
driver_dead = False
study_url = None  # 进入课程后的学习页地址，用于从首页自动返回


def mark_driver_error(e):
    """记录 Selenium 会话失效，避免脚本无提示地卡死。"""
    global driver_dead
    text = str(e)
    if ('no such window' in text
            or 'target window already closed' in text
            or 'invalid session id' in text
            or 'web view not found' in text):
        if not driver_dead:
            print('\n[错误] 浏览器窗口已关闭或 Selenium 会话已失效，脚本无法继续。')
            print('请关闭当前脚本和 Edge 后重新运行。')
        driver_dead = True


def alert():  # 处理课堂测验、弹题和安全验证提示
    global last_alert_time, security_warned
    now = time.time()
    if now - last_alert_time < 1.0:
        time.sleep(0.1)
        return
    last_alert_time = now

    # 先尝试用较通用的方式处理课堂测验/弹题
    try:
        handled = open_edge.execute_script(r"""
            function isVisible(el) {
                if (!el) return false;
                const s = window.getComputedStyle(el);
                return s.display !== 'none' && s.visibility !== 'hidden' && el.getClientRects().length > 0;
            }

            // 用 Vue 组件自带的 handleClose 关闭 AI 随堂练习弹窗
            function closeAiClassExerciseDialog(dialogEl) {
                const appEl = document.querySelector('#app');
                const app = appEl && appEl.__vue_app__;
                const root = app && app._container && app._container._vnode && app._container._vnode.component;
                if (root) {
                    const seen = new Set();
                    let called = false;
                    function typeName(t) {
                        try { return t && (t.name || t.__name || t.displayName) || ''; } catch (e) { return ''; }
                    }
                    function visit(vnode) {
                        if (!vnode || seen.has(vnode) || called) return;
                        seen.add(vnode);
                        if (vnode.component) {
                            const inst = vnode.component;
                            const tn = typeName(inst.type);
                            const dlg = inst.subTree && inst.subTree.component;
                            // 优先关闭真正的 AI 随堂练习组件
                            if (/AiClassExerciseDialog/i.test(tn) && dlg && dlg.exposed && typeof dlg.exposed.handleClose === 'function') {
                                dlg.exposed.handleClose();
                                called = true;
                                return;
                            }
                            // 兜底：找任一包含当前弹窗的 ElDialog 组件并调用其 handleClose
                            if (dialogEl && dlg && dlg.exposed && typeof dlg.exposed.handleClose === 'function' && inst.subTree) {
                                try {
                                    const subEl = inst.subTree.el;
                                    if (subEl && subEl.contains && subEl.contains(dialogEl)) {
                                        dlg.exposed.handleClose();
                                        called = true;
                                        return;
                                    }
                                } catch (e) {}
                            }
                            if (inst.subTree) visit(inst.subTree);
                        }
                        const ch = vnode.children;
                        if (Array.isArray(ch)) { for (const c of ch) visit(c); }
                        else if (ch && typeof ch === 'object') { visit(ch); }
                    }
                    visit(root.subTree);
                    if (called) return true;
                }

                // Vue 关闭失败时的兜底：尝试关闭按钮或隐藏遮罩，避免脚本无限循环
                if (dialogEl) {
                    const closeBtn = dialogEl.querySelector('button.el-dialog__headerbtn, .el-dialog__headerbtn, [aria-label="Close"], .close');
                    if (closeBtn && isVisible(closeBtn)) {
                        closeBtn.click();
                        return true;
                    }
                    const overlay = dialogEl.closest('.el-overlay') || dialogEl.closest('.el-overlay-dialog') || dialogEl.parentElement;
                    if (overlay && overlay.style) {
                        overlay.style.display = 'none';
                        overlay.style.pointerEvents = 'none';
                        return true;
                    }
                }
                return false;
            }
            function hasChoiceOptions(el) {
                if (!el || !isVisible(el)) return false;
                const nodes = Array.from(el.querySelectorAll('li,div,label,span,p'));
                return nodes.some(n => {
                    if (!isVisible(n)) return false;
                    const t = (n.innerText || '').replace(/\s+/g, ' ').trim();
                    return /^[A-F][\s\.、:：\)]/.test(t) && t.length < 80;
                });
            }

            function pickRandomOption(el) {
                let candidates = [];
                const selectors = [
                    'svg.icon.topic-option', '.topic-option', '.option', '.option-item',
                    '.el-radio', '.el-radio__input', '.el-checkbox', '.el-checkbox__input',
                    '.answer-item', '[class*="option"]', '[class*="answer"]',
                    'input[type="radio"]', 'input[type="checkbox"]'
                ];
                for (const sel of selectors) {
                    const arr = Array.from(el.querySelectorAll(sel)).filter(isVisible);
                    if (arr.length) { candidates = arr; break; }
                }
                if (!candidates.length) {
                    const all = Array.from(el.querySelectorAll('li,div,label,span,p')).filter(n => {
                        const t = (n.innerText || '').replace(/\s+/g, ' ').trim();
                        return isVisible(n) && /^[A-F][\s\.、:：\)]/.test(t) && t.length < 80;
                    });
                    candidates = all.filter(n => !all.some(m => m !== n && n.contains(m)));
                }
                if (!candidates.length) return false;
                const ab = candidates.filter(n => {
                    const t = (n.innerText || '').replace(/\s+/g, ' ').trim();
                    return /^A[\s\.、:：\)]/.test(t) || /^B[\s\.、:：\)]/.test(t);
                });
                const pool = ab.length ? ab : candidates;
                const chosen = pool[Math.floor(Math.random() * pool.length)];
                try { chosen.scrollIntoView({block: 'center'}); } catch (e) {}
                const clickTarget = chosen.closest('label,button,div,li') || chosen;
                try { clickTarget.click(); } catch (e) { chosen.click(); }
                return true;
            }


            const keywords = /课堂测验|随堂测验|测验|弹题|答题|题目|未作答|AI随堂练习|随堂练习|提交作答|判断题|多选题|选择题|单选题|请选择|不能关闭|作业|考试/;
            const boxes = Array.from(document.querySelectorAll(
                '#playTopic-dialog, [role="dialog"], .el-dialog, .el-message-box, ' +
                '[class*="dialog"], [class*="popup"], [class*="exam"], [class*="question"]'
            ))
                .filter(isVisible)
                .filter(d => !d.closest('.yidun_modal'));
            const dialog = boxes.find(d =>
                d.id === 'playTopic-dialog'
                || d.classList.contains('ai-class-exercise-dialog')
                || hasChoiceOptions(d)
                || keywords.test(d.innerText || '')
            );
            if (!dialog) return false;

            // 用题目内容做签名，避免同一个弹窗被无限重复提交
            const rawText = (dialog.innerText || '')
                .replace(/已提交/g, '')
                .replace(/正确答案[：:][\s\S]*$/, '')
                .trim()
                .slice(0, 200);
            const quizSig = rawText || 'quiz';
            if (window.__zhidaoQuizSig !== quizSig) {
                window.__zhidaoQuizSig = quizSig;
                window.__zhidaoQuizHandled = false;
                window.__zhidaoQuizCloseRetryTime = 0;
            }

            // 这个弹窗已经处理过，只尝试关闭，不再重复提交和打印
            if (window.__zhidaoQuizHandled) {
                if (!window.__zhidaoQuizCloseRetryTime || Date.now() - window.__zhidaoQuizCloseRetryTime > 10000) {
                    window.__zhidaoQuizCloseRetryTime = Date.now();
                    closeAiClassExerciseDialog(dialog);
                }
                return false;
            }

            // 刚点完提交的 2.5 秒内不要重复提交
            if (window.__zhidaoQuizSubmitTime && Date.now() - window.__zhidaoQuizSubmitTime < 2500) {
                return true;
            }

            // 已经提交过的答题弹窗，直接关掉，避免挡住后续弹题
            const finishedBtn = dialog.querySelector('button.is-finish');
            if (finishedBtn || /已提交/.test(dialog.innerText || '')) {
                window.__zhidaoQuizHandled = true;
                window.__zhidaoQuizSubmitTime = 0;
                closeAiClassExerciseDialog(dialog);
                return true;
            }

            const choiceDialog = hasChoiceOptions(dialog);
            const picked = pickRandomOption(dialog);

            const buttons = Array.from(dialog.querySelectorAll(
                'button, .el-button, [role="button"], a, .btn, [class*="btn"], [class*="submit"]'
            )).filter(isVisible);
            const submit = buttons.find(b => /提交|确定|确认|完成|交卷|下一题|作答/.test((b.innerText || '').trim()));
            if (submit && (!choiceDialog || picked)) {
                window.__zhidaoQuizHandled = true;
                window.__zhidaoQuizSubmitTime = Date.now();
                submit.click();
                setTimeout(function () { closeAiClassExerciseDialog(dialog); }, 2000);
                return true;
            }

            const close = dialog.querySelector(
                'button.el-dialog__headerbtn, .el-dialog__headerbtn, [aria-label="Close"], [class*="close"], .close'
            );
            if (close) {
                // 选择题必须先选中一个选项，再关闭，否则会提示“未作答不能关闭”
                if (!choiceDialog || picked) {
                    window.__zhidaoQuizHandled = true;
                    close.click();
                    return true;
                }
                window.__zhidaoQuizHandled = true;
                return false;
            }
            window.__zhidaoQuizHandled = true;
            return false;
        """)
        if handled:
            print('已处理课堂测验/弹题')
            time.sleep(1)
            try:
                Movement.play()
                print('测验后继续播放')
            except Exception:
                pass
    except Exception as e:
        mark_driver_error(e)

    # 安全验证只检测并提示，不自动绕过
    try:
        yidun = open_edge.execute_script(
            "return document.querySelector('.yidun_modal__header') !== null;"
        )
        if yidun:
            if not security_warned:
                print('检测到安全验证，请手动完成后脚本会继续...')
                security_warned = True
        else:
            security_warned = False
    except Exception:
        pass
    time.sleep(0.2)


def enter():
    # 关闭课堂公告/弹窗；找不到就跳过，避免脚本因为页面改版直接退出
    open_edge.implicitly_wait(3)
    try:
        open_edge.find_element(By.XPATH, '//*[@id="app"]/div/div[6]/div[2]/div[1]/i').click()  # 弹窗
    except Exception:
        print('未找到课堂弹窗，跳过')

    # 等待旧版视频列表或新版播放器加载，最多等 180 秒，给诚信声明确认留时间
    try:
        WebDriverWait(open_edge, 180, 0.5).until(
            ec.presence_of_element_located(
                (By.XPATH, '//li[contains(@class,"clearfix video")] | //*[@id="vjs_container_html5_api"]')
            )
        )
    except Exception:
        print('没有找到视频列表或播放器，请手动点击一个视频，脚本会继续监控测验弹窗。')
        return

    old_videos = open_edge.find_elements(By.XPATH, '//li[contains(@class,"clearfix video")]')
    if not old_videos:
        # 新版页面：已经直接进入视频播放页
        print('检测到新版视频页面，直接播放当前视频')
        try:
            Movement.close_voice()
            print('静音')
        except Exception:
            print('关闭声音失败，跳过')
        try:
            Movement.play()
            print('播放')
        except Exception:
            print('播放失败，请手动点击播放。')
        return

    unfinished_videos = open_edge.find_elements(
        By.XPATH,
        '//li[contains(@class,"clearfix video") and not(.//b[contains(@class,"time_icofinish")])]'
    )
    target = unfinished_videos[0] if unfinished_videos else old_videos[0]

    try:
        icons = target.find_elements(
            By.XPATH,
            './/b[contains(@class,"time_ico") and not(contains(@class,"time_icofinish"))]'
        )
        if icons:
            icons[0].click()
        else:
            target.click()
    except Exception:
        try:
            open_edge.execute_script("arguments[0].click();", target)
        except Exception:
            print('点击视频失败，请手动点击一个视频。')
            return

    time.sleep(1)
    try:
        Movement.close_voice()
        print('静音')
    except Exception:
        print('关闭声音失败，跳过')
    try:
        Movement.play()
        print('播放')
    except Exception:
        print('播放失败，请手动点击播放。')


def watch():
    while True:
        event2.wait()
        try:
            open_edge.implicitly_wait(2)
            old_finished = open_edge.find_elements(
                By.XPATH,
                '//li[contains(@class,"clearfix video") and contains(@class,"current_play")]'
                '//b[contains(@class,"time_icofinish")]'
            )
            if old_finished:
                Movement.next()
                Movement.close_voice()
                Movement.play()
        except Exception:
            pass
        event2.clear()
        event1.set()


def install_auto_play():
    """新版智慧树播放器兜底：暂停自动播、结束自动调用站点 nextVideo。"""
    js = r"""
        if (!window.__zhidaoAutoNextTimer) {
            function callVideoNext() {
                const appEl = document.querySelector('#app');
                const app = appEl && appEl.__vue_app__;
                const root = app && app._container && app._container._vnode && app._container._vnode.component;
                if (!root) return false;
                const seen = new Set();
                let called = false;
                function typeName(t) {
                    try { return t && (t.name || t.__name || t.displayName) || ''; } catch (e) { return ''; }
                }
                function visit(vnode) {
                    if (!vnode || seen.has(vnode) || called) return;
                    seen.add(vnode);
                    if (vnode.component) {
                        const inst = vnode.component;
                        if (typeName(inst.type) === 'VideoCom' && inst.exposed && typeof inst.exposed.nextVideo === 'function') {
                            inst.exposed.nextVideo();
                            called = true;
                            return;
                        }
                        if (inst.subTree) visit(inst.subTree);
                    }
                    const ch = vnode.children;
                    if (Array.isArray(ch)) { for (const c of ch) visit(c); }
                    else if (ch && typeof ch === 'object') { visit(ch); }
                }
                visit(root.subTree);
                return called;
            }

            function hasVisibleQuestionDialog() {
                const nodes = Array.from(document.querySelectorAll(
                    '.ai-class-exercise-dialog, #playTopic-dialog, .el-dialog, [class*="dialog"], [class*="popup"], [class*="exam"]'
                ));
                return nodes.some(function (d) {
                    if (!d || d.getClientRects().length === 0) return false;
                    const text = (d.innerText || '').replace(/\s+/g, ' ');
                    return /课堂测验|随堂|测验|弹题|答题|题目|选择题|单选题|多选题|判断题|未作答|提交作答|作答|不能关闭/.test(text);
                });
            }

            window.__zhidaoNextLocked = false;
            window.__zhidaoAutoNextTimer = setInterval(function () {
                var v = document.querySelector('video');
                if (!v) return;
                var quizVisible = hasVisibleQuestionDialog();
                if (quizVisible) return;

                if (v.ended) {
                    if (!window.__zhidaoNextLocked) {
                        window.__zhidaoNextLocked = true;
                        callVideoNext();
                    }
                    return;
                }

                window.__zhidaoNextLocked = false;
                if (v.paused && v.readyState >= 2) {
                    v.muted = true;
                    v.play().catch(function () {});
                }
            }, 1000);
        }
    """
    try:
        open_edge.execute_script(js)
        print('已开启视频自动继续/自动下一节')
    except Exception:
        print('开启视频自动继续失败，跳过')


def ensure_study_page():
    """如果页面意外跳到智慧树主页，自动返回刚才的课程学习页。"""
    global study_url
    if not study_url:
        return
    try:
        current_url = open_edge.current_url
    except Exception:
        current_url = ''
    if ('wisdom-mooc.zhihuishu.com/study' in current_url
            or 'studyvideoh5.zhihuishu.com/stuStudy' in current_url):
        return
    # 只处理明显跳到智慧树主页的情况，避免干扰其他页面
    if not (
        current_url.startswith('https://www.zhihuishu.com')
        or current_url.rstrip('/') == 'https://wisdom-mooc.zhihuishu.com'
        or current_url.startswith('https://onlineweb.zhihuishu.com/onlinestuh5')
        or current_url.rstrip('/') == 'https://onlineweb.zhihuishu.com'
        or current_url.rstrip('/') == 'https://studyvideoh5.zhihuishu.com'
    ):
        return

    print('检测到页面跳到了主页，正在自动返回课程页...')
    # 先尝试浏览器后退
    try:
        open_edge.back()
        time.sleep(2)
    except Exception:
        pass
    try:
        current_url = open_edge.current_url
    except Exception:
        current_url = ''
    # 后退无效则直接打开保存的学习页
    if ('wisdom-mooc.zhihuishu.com/study' not in current_url
            and 'studyvideoh5.zhihuishu.com/stuStudy' not in current_url):
        try:
            open_edge.get(study_url)
        except Exception:
            pass
    # 立即安装：页面加载后如果检测到视频已结束，会调用站点 nextVideo
    try:
        install_auto_play()
    except Exception:
        pass
    # 等播放器/侧边栏回来
    try:
        WebDriverWait(open_edge, 15, 0.5).until(
            lambda d: d.find_elements(By.ID, 'vjs_container_html5_api')
            or d.find_elements(By.CSS_SELECTOR, '.chapter-content-second')
            or d.find_elements(By.ID, 'playButton')
        )
    except Exception:
        pass
    try:
        install_auto_play()
    except Exception:
        pass


def reset_study_flow():
    """按回车后重新进入当前课程，保留已选课程和登录状态。"""
    global study_url
    print('\n[重置] 收到回车，正在重新进入当前课程...')
    event2.clear()
    time.sleep(0.3)
    try:
        if not study_url:
            study_url = open_edge.current_url
        try:
            open_edge.get(study_url)
        except Exception:
            open_edge.refresh()
        open_edge.implicitly_wait(3)
        try:
            install_auto_play()
        except Exception:
            pass
        try:
            WebDriverWait(open_edge, 15, 0.5).until(
                lambda d: d.find_elements(By.ID, 'vjs_container_html5_api')
                or d.find_elements(By.CSS_SELECTOR, '.chapter-content-second')
                or d.find_elements(By.ID, 'playButton')
            )
        except Exception:
            pass
        try:
            install_auto_play()
        except Exception:
            pass
        try:
            Movement.close_voice()
        except Exception:
            pass
        try:
            Movement.play()
        except Exception:
            pass
        print('[重置] 完成，继续学习。\n')
    except Exception as e:
        print(f'[重置] 失败：{e}')
        mark_driver_error(e)
    finally:
        event2.clear()
        event1.set()


def reset_listener():
    """后台监听命令行输入，按一次回车触发重置。"""
    while True:
        try:
            line = sys.stdin.readline()
        except Exception:
            break
        if line == '':
            break
        # 用户在命令提示符中按下 Enter 就触发
        reset_event.set()
        event1.set()


def start_reset_listener():
    listener = threading.Thread(target=reset_listener, daemon=True)
    listener.start()
    print('\n提示：自动学习过程中按 Enter 键可重置当前课程播放流程（不会重新登录或重新选课）。')


alert()
# 进入课堂
enter()
try:
    study_url = open_edge.current_url
except Exception:
    study_url = None
install_auto_play()
start_reset_listener()
thread = threading.Thread(target=watch, daemon=True).start()

event1.set()
while True:
    if driver_dead:
        print('\n脚本已停止：浏览器会话失效，请重新运行。')
        break
    if reset_event.is_set():
        reset_event.clear()
        reset_study_flow()
        continue
    ensure_study_page()
    try:
        all_courses = open_edge.find_elements(By.XPATH, '//li[contains(@class,"clearfix video")]')
        all_finish = open_edge.find_elements(
            By.XPATH,
            '//li[contains(@class,"clearfix video")]//b[contains(@class,"time_icofinish")]'
        )
    except Exception as e:
        mark_driver_error(e)
        all_courses, all_finish = [], []
    if all_courses and len(all_courses) == len(all_finish):
        open_edge.quit()
        print('已完成所有的课程')
        break
    else:
        event1.wait()
        if reset_event.is_set():
            reset_event.clear()
            reset_study_flow()
            continue
        alert()
        try:
            if not open_edge.execute_script("return !!window.__zhidaoAutoNextTimer;"):
                install_auto_play()
        except Exception:
            pass
        event1.clear()
        event2.set()
