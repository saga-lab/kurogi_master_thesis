修論，卒論 TeXファイル サンプル
作成 2011/1/27
作成者 阿部 佑樹 (mail:kituto@gmail.com)


main.tex                メインのTeXファイル
[1-6].tex,thanks.tex    各章のtexファイル
ref.bib                 参考文献を記述するファイル

kupaper.cls         クラスファイル
jtygm.sty            Texコンパイル時のFont Warningを抑制


fig


TeXファイルを開き，C-c t j でplatexでコンパイルを行う．
bibtexを使っている場合，C-c t bで jbibtexコンパイル


platex->jbibtex->platex->platexを繰り返す．
めんどくさい人は OMakeを検索してみてください．



以下，.emacsに追記するとうれしいかも．

;;;;;;;;;;ここから;;;;;;;;;;;;
(autoload 'yatex-mode "yatex" "Yet Another LaTeX mode" t)
(setq auto-mode-alist
      (cons (cons "\\.tex$" 'yatex-mode) auto-mode-alist))
;  YaTeX-kanji-code 3   ; (1 SJIS, 2 JIS, 3 EUC 4 UTF-8) JIS(junet-unix)だとOS依存せ
;;ずにコンパイルできる
(setq YaTeX-kanji-code 3) ;; Vine ならEUC Ubuntu使ってて分かっている人は4
(setq YaTeX-latex-message-code 'euc-jp)

;; Footer部の Local CariablesのWarningを抑制
;; % Local Variables:
;; % TeX-master: t
;; % mode: yatex
;; % End:
(put 'TeX-master 'safe-local-variable
     (lambda (x)
       (or (stringp x)
              (member x (quote (t nil shared dwim))))))


(setq tex-command "platex")
;;(setq tex-command "platex -src-specials") ;;dvi-preview使う場合は必要
(setq dvi2-command "xdvi")        ;;C-c t pでdviプレビュー
(setq bibtex-command "jbibtex")   ;;C-c t bでbibコンパイル
(setq dviprint-command-format "dvipdfmx %s");;C-c t lでpdfコンバート


;;;;;dvi-preview
;; ;;最初に起動した emacs だけ server-start するには [ここ] より
;; (require 'server)
;; (unless (server-running-p)
;;        (server-start))

;; (require 'xdvi-search) ; 必須
;; ;; 窓を上に
;; (add-hook 'yatex-mode-hook
;;           '(lambda ()
;;              (define-key YaTeX-mode-map "\C-c\C-j" 'xdvi-jump-to-line)
;;              (auto-fill-mode t) (setq fill-column 80) ))

;;;;;;;;;;ここまで;;;;;;;;;;;;

