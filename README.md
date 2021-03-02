# project
school_project_tranagor


// MFCmyProectDlg.cpp: файл реализации
//

#include "pch.h"
#include "framework.h"
#include "MFCmyProect.h"
#include "MFCmyProectDlg.h"
#include "afxdialogex.h"

#ifdef _DEBUG
#define new DEBUG_NEW
#endif


// Диалоговое окно CAboutDlg используется для описания сведений о приложении

class CAboutDlg : public CDialogEx
{
public:
	CAboutDlg();

// Данные диалогового окна
#ifdef AFX_DESIGN_TIME
	enum { IDD = IDD_ABOUTBOX };
#endif

	protected:
	virtual void DoDataExchange(CDataExchange* pDX);    // поддержка DDX/DDV

// Реализация
protected:
	DECLARE_MESSAGE_MAP()
};

CAboutDlg::CAboutDlg() : CDialogEx(IDD_ABOUTBOX)
{
}

void CAboutDlg::DoDataExchange(CDataExchange* pDX)
{
	CDialogEx::DoDataExchange(pDX);
}

BEGIN_MESSAGE_MAP(CAboutDlg, CDialogEx)
END_MESSAGE_MAP()


// Диалоговое окно CMFCmyProectDlg



CMFCmyProectDlg::CMFCmyProectDlg(CWnd* pParent /*=nullptr*/)
	: CDialogEx(IDD_MFCMYPROECT_DIALOG, pParent)
{
	m_hIcon = AfxGetApp()->LoadIcon(IDR_MAINFRAME);
}

void CMFCmyProectDlg::DoDataExchange(CDataExchange* pDX)
{
	CDialogEx::DoDataExchange(pDX);
	//  DDX_Control(pDX, IDC_EDIT1, m_okno);
}

BEGIN_MESSAGE_MAP(CMFCmyProectDlg, CDialogEx)
	ON_WM_SYSCOMMAND()
	ON_WM_PAINT()
	ON_WM_QUERYDRAGICON()
	ON_COMMAND(ID_BASCHNJA, &CMFCmyProectDlg::OnBaschnja)
	ON_WM_KEYDOWN()
//	ON_WM_SYSKEYDOWN()
ON_WM_CHAR()
ON_WM_UNICHAR()
ON_COMMAND(ID_32774, &CMFCmyProectDlg::OnAbout)
ON_COMMAND(ID_32773, &CMFCmyProectDlg::OnBaschnjaPrawila)
//ON_COMMAND(ID_32775, &CMFCmyProectDlg::OnThor)
ON_COMMAND(ID_THOR_L, &CMFCmyProectDlg::OnThorL)
ON_COMMAND(ID_THOR_SR, &CMFCmyProectDlg::OnThorSr)
ON_COMMAND(ID_THOR_SL, &CMFCmyProectDlg::OnThorSl)
ON_WM_TIMER()
ON_COMMAND(ID_THOR_PRAVILA, &CMFCmyProectDlg::OnThorPravila)
ON_COMMAND(ID_FEANOR_L, &CMFCmyProectDlg::OnFeanorL)
ON_COMMAND(ID_FEANOR_S, &CMFCmyProectDlg::OnFeanorS)
ON_COMMAND(ID_FEANOR_PR, &CMFCmyProectDlg::OnFeanorPr)
ON_WM_SYSKEYDOWN()
END_MESSAGE_MAP()


// Обработчики сообщений CMFCmyProectDlg

BOOL CMFCmyProectDlg::OnInitDialog()
{
	CDialogEx::OnInitDialog();

	// Добавление пункта "О программе..." в системное меню.

	// IDM_ABOUTBOX должен быть в пределах системной команды.
	ASSERT((IDM_ABOUTBOX & 0xFFF0) == IDM_ABOUTBOX);
	ASSERT(IDM_ABOUTBOX < 0xF000);

	CMenu* pSysMenu = GetSystemMenu(FALSE);
	if (pSysMenu != nullptr)
	{
		BOOL bNameValid;
		CString strAboutMenu;
		bNameValid = strAboutMenu.LoadString(IDS_ABOUTBOX);
		ASSERT(bNameValid);
		if (!strAboutMenu.IsEmpty())
		{
			pSysMenu->AppendMenu(MF_SEPARATOR);
			pSysMenu->AppendMenu(MF_STRING, IDM_ABOUTBOX, strAboutMenu);
		}
	}

		// Задает значок для этого диалогового окна.  Среда делает это автоматически,
	//  если главное окно приложения не является диалоговым
	SetIcon(m_hIcon, TRUE);			// Крупный значок
	SetIcon(m_hIcon, FALSE);		// Мелкий значок

	// TODO: добавьте дополнительную инициализацию
	X = GetSystemMetrics(SM_CXSCREEN);  Y = GetSystemMetrics(SM_CYSCREEN) - 50;
	CZastawcaDlg z;
	z.DoModal();

	return TRUE;  // возврат значения TRUE, если фокус не передан элементу управления
}

void CMFCmyProectDlg::OnSysCommand(UINT nID, LPARAM lParam)
{
	if ((nID & 0xFFF0) == IDM_ABOUTBOX)
	{
		CAboutDlg dlgAbout;
		dlgAbout.DoModal();
	}
	else
	{
		CDialogEx::OnSysCommand(nID, lParam);
	}
}

// При добавлении кнопки свертывания в диалоговое окно нужно воспользоваться приведенным ниже кодом,
//  чтобы нарисовать значок.  Для приложений MFC, использующих модель документов или представлений,
//  это автоматически выполняется рабочей областью.

void CMFCmyProectDlg::OnPaint()
{
	if (IsIconic())
	{
		CPaintDC dc(this); // контекст устройства для рисования

		SendMessage(WM_ICONERASEBKGND, reinterpret_cast<WPARAM>(dc.GetSafeHdc()), 0);

		// Выравнивание значка по центру клиентского прямоугольника
		int cxIcon = GetSystemMetrics(SM_CXICON);
		int cyIcon = GetSystemMetrics(SM_CYICON);
		CRect rect;
		GetClientRect(&rect);
		int x = (rect.Width() - cxIcon + 1) / 2;
		int y = (rect.Height() - cyIcon + 1) / 2;

		// Нарисуйте значок
		dc.DrawIcon(x, y, m_hIcon);
	}
	else
	{
		CDialogEx::OnPaint();
	}
}

// Система вызывает эту функцию для получения отображения курсора при перемещении
//  свернутого окна.
HCURSOR CMFCmyProectDlg::OnQueryDragIcon()
{
	return static_cast<HCURSOR>(m_hIcon);
}



void CMFCmyProectDlg::OnBaschnja()
{
	// TODO: добавьте свой код обработчика команд

	CMenu* pMenu = GetMenu();
	pMenu->EnableMenuItem(ID_THOR_L, MF_GRAYED);
	pMenu->EnableMenuItem(ID_THOR_SR, MF_GRAYED);
	pMenu->EnableMenuItem(ID_THOR_SL, MF_GRAYED);
	pMenu->EnableMenuItem(ID_FEANOR_L, MF_GRAYED); 
	pMenu->EnableMenuItem(ID_FEANOR_S, MF_GRAYED);

	ifsau = 1;
	int kx = X / 20;
	int ky = Y / 20;
	CClientDC dc(this);//один раз на функцию
	CBrush mybrush;
	CBrush* pOldBrush;
	mybrush.CreateSolidBrush(RGB(255, 255, 255));//255 255 255 белый, 0 0 0 черный
	pOldBrush = dc.SelectObject(&mybrush);
	MoveWindow(0, 0, X, Y, TRUE);
	dc.Rectangle(0, 0, X, Y);
	dc.SelectObject(pOldBrush);//удаление кисточки (+ строка ниже)
	mybrush.DeleteObject();

	CPen hpen;
	CPen* pOldPen;
	hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
	pOldPen = dc.SelectObject(&hpen);
	dc.MoveTo(0,0);
	dc.LineTo(X, 0);
	
	CFont MyFont;

	
	mybrush.CreateSolidBrush(RGB(0, 0, 0));
	pOldBrush = dc.SelectObject(&mybrush);

	dc.Rectangle((X-X/4) / 2 - kx / 2, Y - ky - 60, (X-X/4) / 2 + kx / 2, Y - 60);
	int xwerh, ywerh, xniz, yniz;
	xwerh = (X - X / 4) / 2 - kx / 2; ywerh = Y - ky - 60;
	xniz = (X - X / 4) / 2 - kx / 2; yniz = Y - 60;

	//minibaschenka 1 kirpitschik
	dc.SelectObject(pOldBrush);
	mybrush.DeleteObject();

	mybrush.CreateSolidBrush(RGB(166, 111, 111));
	pOldBrush = dc.SelectObject(&mybrush);
	dc.Rectangle(X-X/4, Y-60-Y/2-Y/4-ky/2, X, Y-60-Y/2);
	dc.SelectObject(pOldBrush);
	mybrush.DeleteObject();

	mybrush.CreateSolidBrush(RGB(0, 0, 0));
	pOldBrush = dc.SelectObject(&mybrush);
	int minixwerh, miniywerh;
	minixwerh = (X - X / 8)-(kx/4); miniywerh = ((Y - 60) -Y/2)-ky/2;
	dc.Rectangle(minixwerh, miniywerh, minixwerh+ kx / 2, miniywerh+ky/2);
	//
	int stop,K,rast, l;
	TCHAR s[10];

	HBITMAP hb;
	HDC hMemDC;
	dc.SelectObject(pOldBrush);
	mybrush.DeleteObject();
	mybrush.CreateSolidBrush(RGB(32, 0, 32));
	pOldBrush = dc.SelectObject(&mybrush);
	dc.Rectangle(X - 40 - 348, Y - 60 -40 - 301,  X, Y - 60 );

	hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_SAURON));
	hMemDC = ::CreateCompatibleDC(NULL);
	SelectObject(hMemDC, hb);
	::StretchBlt(dc.m_hDC, X-20-348, Y-60-20-301, 348, 301,//адресат-экран
		hMemDC, 0, 0, 348, 301, SRCCOPY); //источник

	::DeleteDC(hMemDC);
	::DeleteObject(hb);
	int i;
	for (i=1;i<=10;i++)
	{ 
	 stop = a();	
	 K = padenie(stop, xwerh, ywerh);
	 if (K == 0)
	 { 
	 hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_OKO_FATAL));
	 hMemDC = ::CreateCompatibleDC(NULL);
	 SelectObject(hMemDC, hb);
	 ::StretchBlt(dc.m_hDC, 0, 0, X, Y-60,//адресат-экран
		 hMemDC, 0, 0, 1324, 814, SRCCOPY); //источник

	 ::DeleteDC(hMemDC);
	 ::DeleteObject(hb);
	 dc.SetBkMode(TRANSPARENT);
	 MyFont.CreateFont(Y/10, 0, 0, 0, 700, FALSE, FALSE, 0, ANSI_CHARSET,
		 OUT_DEFAULT_PRECIS, CLIP_DEFAULT_PRECIS,
		 DEFAULT_QUALITY, DEFAULT_PITCH | FF_SWISS,
		 L"Arial"); 
	 dc.SelectObject(&MyFont);
	 dc.SetTextColor(RGB(248, 242, 16));
	 dc.TextOut(X/2-70,Y/2,L"ВЫ ПРОИГРАЛИ...");
	   break;
	 }
	 //подсчет кирпичиков вывод
	 dc.SelectObject(pOldBrush); mybrush.DeleteObject();
	 mybrush.CreateSolidBrush(RGB(242, 242, 57));
	 pOldBrush = dc.SelectObject(&mybrush);
	 int xx = X - X / 4 + X / 8 - 30;
	 dc.Rectangle(xx, (Y-60-Y/2-Y/4-ky/2)/2-20, xx + 60, (Y - 60 - Y / 2 - Y / 4 - ky / 2) / 2 + 20);
	 dc.SetBkMode(TRANSPARENT); //прозрачный фон
	 swprintf_s(s, L"%d/10", i);
	 dc.TextOut(xx+10, (Y - 60 - Y / 2 - Y / 4 - ky / 2) / 2 - 10, s);
	 dc.SelectObject(pOldBrush); mybrush.DeleteObject();
	 mybrush.CreateSolidBrush(RGB(0, 0, 0));
	 pOldBrush = dc.SelectObject(&mybrush);

	// вызов башенки  и поменять миниверх
	rast = abs(stop - xwerh); if (stop >= xwerh) l = 0; else l = 1;
	minixwerh = baschenka(rast, minixwerh, miniywerh, l);
	miniywerh -= ky / 2;
	//
	//сдвиг кирпичей вниз
	if (i > 1)
	{
		int sk = 0;
		while (ywerh < yniz)
		{
			sk++;
			dc.MoveTo(stop, ywerh - ky);
			dc.LineTo(stop + kx, ywerh - ky);
			dc.MoveTo(xwerh, ywerh);
			dc.LineTo(xwerh + kx, ywerh);
			dc.MoveTo(xniz, ywerh + ky);
			dc.LineTo(xniz + kx, ywerh + ky);
			ywerh++;
			dc.Rectangle(stop, ywerh - ky, stop + kx, ywerh);
			dc.Rectangle(xwerh, ywerh, xwerh + kx, ywerh + ky);
			dc.Rectangle(xniz, ywerh + ky, xniz + kx, ywerh + ky + ky - sk);
			Sleep(5);
		}
	}
	// 
	upal = 0;
	  if (K == 1) 
	  { xniz = xwerh; xwerh = stop;yniz= ywerh; ywerh = ywerh- ky; }
	  	
	}
	if (i == 11)
	{
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_OKO1));
		hMemDC = ::CreateCompatibleDC(NULL);
		SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, 0, 0, X, Y - 60,//адресат-экран
			hMemDC, 0, 0, 1232, 816, SRCCOPY); //источник
		::DeleteDC(hMemDC);
		::DeleteObject(hb);
		Sleep(500);
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_OKO2));
		hMemDC = ::CreateCompatibleDC(NULL);
		SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, 0, 0, X, Y - 60,//адресат-экран
			hMemDC, 0, 0, 1324, 814, SRCCOPY); //источник
		::DeleteDC(hMemDC);
		::DeleteObject(hb);
		Sleep(500);
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_OKO3));
		hMemDC = ::CreateCompatibleDC(NULL);
		SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, 0, 0, X, Y - 60,//адресат-экран
			hMemDC, 0, 0, 1324, 814, SRCCOPY); //источник
		::DeleteDC(hMemDC);
		::DeleteObject(hb);
		dc.SetBkMode(TRANSPARENT);
		MyFont.CreateFont(Y / 7, 0, 0, 0, 700, FALSE, FALSE, 0, ANSI_CHARSET,
			OUT_DEFAULT_PRECIS, CLIP_DEFAULT_PRECIS,
			DEFAULT_QUALITY, DEFAULT_PITCH | FF_SWISS,
			L"Arial");
		dc.SelectObject(&MyFont);
		dc.SetTextColor(RGB(255, 0, 0));
		dc.TextOut(50, (Y-60)/2, L"УРА!");
		dc.TextOut(50, (Y-60) / 2+Y/7+20, L"ПОБЕДА!");

	}
	ifsau = 0;
	upal = 0;
	dc.SelectObject(pOldBrush);
	mybrush.DeleteObject();
	dc.SelectObject(pOldPen);hpen.DeleteObject();
	pMenu->EnableMenuItem(ID_THOR_L, MF_ENABLED);
	pMenu->EnableMenuItem(ID_THOR_SR, MF_ENABLED);
	pMenu->EnableMenuItem(ID_THOR_SL, MF_ENABLED);
	pMenu->EnableMenuItem(ID_FEANOR_L, MF_ENABLED);
	pMenu->EnableMenuItem(ID_FEANOR_S, MF_ENABLED);
}



int CMFCmyProectDlg::a()
{
	int kx = X / 20;
	int ky = Y / 20;

	CClientDC dc(this);
	CBrush mybrush;
	CBrush* pOldBrush;
	mybrush.CreateSolidBrush(RGB(0, 0, 0));
	pOldBrush = dc.SelectObject(&mybrush);

	dc.Rectangle(0, 0, kx, ky);

	CPen hpen;
	CPen* pOldPen;
	hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
	pOldPen = dc.SelectObject(&hpen);
	MSG mes;
	int x = 0, key = 1;

	while (upal == 0)
	{
		if (x + 1 + kx > X-X/4) key = 0;
		if (x - 1 < 0) key = 1;

		if (PeekMessage(&mes, NULL, 0, 0, PM_REMOVE))
		{
			TranslateMessage(&mes);
			DispatchMessage(&mes);
		}

		if ((x + 1 + kx <= X-X/4) && key)
		{
			//sdwig wprawo

			dc.MoveTo(x, 0);
			dc.LineTo(x, ky);
			x ++;
			dc.Rectangle(x, 0, x + kx, ky);
			Sleep(5);

		}
		if ((x > 0) && (!key))
		{
			//sdwig wlewo
			dc.MoveTo(x, 0);
			dc.LineTo(x, ky);
			x --;
			dc.Rectangle(x, 0, x + kx, ky);
			Sleep(5);
		}
	}
	dc.SelectObject(pOldBrush);	mybrush.DeleteObject();
	dc.SelectObject(pOldPen);	hpen.DeleteObject();
	
	return x;
}


int CMFCmyProectDlg::padenie(int x, int xwerh, int ywerh)
{
	int kx = X / 20;
	int ky = Y / 20;
	int y = ky;
	CClientDC dc(this);
	CBrush mybrush;
	CBrush* pOldBrush;
	mybrush.CreateSolidBrush(RGB(0, 0, 0));
	pOldBrush = dc.SelectObject(&mybrush);
	CPen hpen;
	CPen* pOldPen;
	hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
	pOldPen = dc.SelectObject(&hpen);

	while (y < ywerh)
	{
		dc.MoveTo(x, y - ky);
		dc.LineTo(x + kx, y - ky);
		y++;
		dc.Rectangle(x, y - ky, x + kx, y);
		Sleep(3);
	}
	int rast = abs(x - xwerh);
	if (kx / 2 >= rast)
	{
		dc.SelectObject(pOldBrush);
		mybrush.DeleteObject();
		dc.SelectObject(pOldPen);
		hpen.DeleteObject();
		return 1;
	}
	if (rast >= kx)
	{
		while (y < Y - 60 +ky)
		{
			dc.MoveTo(x, y - ky);
			dc.LineTo(x + kx, y - ky);
			y++;
			dc.Rectangle(x, y - ky, x + kx, y);
			Sleep(3);
		}
		dc.SelectObject(pOldBrush);
		mybrush.DeleteObject();
		dc.SelectObject(pOldPen);
		hpen.DeleteObject();
		return 0;
	}
	
		kuwirk(x,  xwerh,  ywerh);
		dc.SelectObject(pOldBrush);
		mybrush.DeleteObject();
		dc.SelectObject(pOldPen);
		hpen.DeleteObject();
		return 0;
	
}

void CMFCmyProectDlg::OnKeyDown(UINT nChar, UINT nRepCnt, UINT nFlags)
{
	if (ifsau == 1) {
		if (nChar == 32)
		upal = 1;
		//upal=0 после удачного завершения падения, сдвига и рисования мини-башенки!!!!
		//MessageBox(L"OK", L"onKeyDown", MB_OK);
		
	}
	if (iffea == 1) {
		if (nChar == 38)
			feapw = 1;
		
	}
	if (ifthor == 1)
	{
		switch(nChar)
		{ case 16:
			Mjo = 1;
			//MessageBox(L"Mjolnir", L"onKeyDown", MB_OK);
			break;
		
		  case 37:
			//MessageBox(L"left", L"onKeyDown", MB_OK);
			l = 1;
			break;
		  case 39:		
			//MessageBox(L"right", L"onKeyDown", MB_OK);
			r = 1;
			break;
		  default: break;
		}

	}
	CDialogEx::OnKeyDown(nChar, nRepCnt, nFlags);
}

void CMFCmyProectDlg::kuwirk(int x, int xwerh, int ywerh)
{
	int kx = X / 20;
	int ky = Y / 20;
	CClientDC dc(this);
	CBrush mybrush;
	CBrush* pOldBrush;
	mybrush.CreateSolidBrush(RGB(0, 0, 0));
	pOldBrush = dc.SelectObject(&mybrush);
	CPen hpen;
	CPen* pOldPen;
	hpen.CreatePen(PS_SOLID, 1, RGB(0, 0, 0));
	pOldPen = dc.SelectObject(&hpen);
	int xk = xwerh + kx;
	int a,x1,x2,x3,x4,y1,y2,y3,y4,dx;
	if (x > xwerh) 
	{
		dx = xk-x;
	   for (a = 1;a <= 90;a++)
	   {
		x1 = xk - dx * cos(a / rg);
		y1 = ywerh - dx * sin(a / rg);
		x2 = x1 + ky * cos((90 - a) / rg);
		y2=y1-ky* sin((90 - a) / rg);
		x3=x2+kx* sin((90 - a) / rg);
		y3=y2+kx* cos((90 - a) / rg);
		x4=x3-ky* cos((90 - a) / rg);
		y4=y3+ky* sin((90 - a) / rg);
		//risovanie kirpitscha
        dc.MoveTo(x1, y1);
		dc.LineTo(x2, y2);		
		dc.LineTo(x3, y3);
		dc.LineTo(x4, y4);
		dc.LineTo(x1, y1);
		dc.ExtFloodFill(x1 + (x3 - x1) / 2, y2 + (y4 - y2) / 2, RGB(0, 0, 0), FLOODFILLBORDER);
			Sleep(3);
		//stiranie kirpitscha
			dc.SelectObject(pOldBrush);
			mybrush.DeleteObject();
			mybrush.CreateSolidBrush(RGB(255, 255, 255));pOldBrush = dc.SelectObject(&mybrush);
			dc.SelectObject(pOldPen);
			hpen.DeleteObject();
			hpen.CreatePen(PS_SOLID, 1, RGB(22, 14, 14));pOldPen = dc.SelectObject(&hpen);
			dc.MoveTo(x1, y1);
			dc.LineTo(x2, y2);
			dc.LineTo(x3, y3);
			dc.LineTo(x4, y4);
			dc.LineTo(x1, y1);
			dc.ExtFloodFill(x1 + (x3 - x1) / 2, y2 + (y4 - y2) / 2, RGB(22, 14, 14), FLOODFILLBORDER);
			dc.SelectObject(pOldPen);
			hpen.DeleteObject();
			hpen.CreatePen(PS_SOLID, 1, RGB(255,255, 255));pOldPen = dc.SelectObject(&hpen);
			dc.MoveTo(x1, y1);
			dc.LineTo(x2, y2);
			dc.LineTo(x3, y3);
			dc.LineTo(x4, y4);
			dc.LineTo(x1, y1);
			dc.SelectObject(pOldBrush);
			mybrush.DeleteObject();
			dc.SelectObject(pOldPen);
			hpen.DeleteObject();
			mybrush.CreateSolidBrush(RGB(0, 0, 0));pOldBrush = dc.SelectObject(&mybrush);
			hpen.CreatePen(PS_SOLID, 1, RGB(0, 0, 0));pOldPen = dc.SelectObject(&hpen);
	   }
	x1 += 2;
	dc.SelectObject(pOldPen);
	hpen.DeleteObject();
	hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));pOldPen = dc.SelectObject(&hpen);
	while (y1 <= Y - 60)
	  {
		dc.MoveTo(x1, y1);
		dc.LineTo(x1 + ky, y1);
		y1++;
		dc.Rectangle(x1, y1, x1 + ky, y1 + kx);
		Sleep(4);
	  }
	}
	else
	{
		dx =x+kx-xwerh;
		for (a = 1;a <= 90;a++)
		{
			x1 = xwerh + dx * cos(a / rg);
			y1 = ywerh - dx * sin(a / rg);
			x2 = x1 - ky * sin(a / rg);
			y2 = y1 - ky * cos(a / rg);
			x3 = x2 - kx * cos(a / rg);
			y3 = y2 + kx * sin(a / rg);
			x4 = x3 + ky * sin(a / rg);
			y4 = y3 + ky * cos(a / rg);
			//risovanie kirpitscha
			dc.MoveTo(x1, y1);
			dc.LineTo(x2, y2);
			dc.LineTo(x3, y3);
			dc.LineTo(x4, y4);
			dc.LineTo(x1, y1);
			dc.ExtFloodFill(x3 + (x1 - x3) / 2, y2 + (y4 - y2) / 2, RGB(0, 0, 0), FLOODFILLBORDER);
			Sleep(3);
			//stiranie kirpitscha
			dc.SelectObject(pOldBrush);
			mybrush.DeleteObject();
			mybrush.CreateSolidBrush(RGB(255, 255, 255));pOldBrush = dc.SelectObject(&mybrush);
			dc.SelectObject(pOldPen);
			hpen.DeleteObject();
			hpen.CreatePen(PS_SOLID, 1, RGB(22, 14, 14));pOldPen = dc.SelectObject(&hpen);
			dc.MoveTo(x1, y1);
			dc.LineTo(x2, y2);
			dc.LineTo(x3, y3);
			dc.LineTo(x4, y4);
			dc.LineTo(x1, y1);
			dc.ExtFloodFill(x3 + (x1 - x3) / 2, y2 + (y4 - y2) / 2, RGB(22, 14, 14), FLOODFILLBORDER);
			dc.SelectObject(pOldPen);
			hpen.DeleteObject();
			hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));pOldPen = dc.SelectObject(&hpen);
			dc.MoveTo(x1, y1);
			dc.LineTo(x2, y2);
			dc.LineTo(x3, y3);
			dc.LineTo(x4, y4);
			dc.LineTo(x1, y1);
			dc.SelectObject(pOldBrush);
			mybrush.DeleteObject();
			dc.SelectObject(pOldPen);
			hpen.DeleteObject();
			mybrush.CreateSolidBrush(RGB(0, 0, 0));pOldBrush = dc.SelectObject(&mybrush);
			hpen.CreatePen(PS_SOLID, 1, RGB(0, 0, 0));pOldPen = dc.SelectObject(&hpen);
		
			//MessageBox(L"OK", L"", MB_OK);
		}
	
	x2-=2;
	dc.SelectObject(pOldPen);
	hpen.DeleteObject();
	hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));pOldPen = dc.SelectObject(&hpen);
	  while (y2 <= Y - 60)
	  {
		dc.MoveTo(x2, y2);
		dc.LineTo(x2 + ky, y2);
		y2++;
		dc.Rectangle(x2, y2, x2 + ky, y2+kx);
		Sleep(4);
	  }
    }
	dc.SelectObject(pOldBrush);
	mybrush.DeleteObject();
	dc.SelectObject(pOldPen);
	hpen.DeleteObject();
}
int CMFCmyProectDlg::baschenka(int rast, int minixwerh, int miniywerh,int l)
{
	int kx = X / 40;
	int ky = Y / 40;
	CClientDC dc(this);
	CBrush mybrush;
	CBrush* pOldBrush;
	mybrush.CreateSolidBrush(RGB(0, 0, 0));
	pOldBrush = dc.SelectObject(&mybrush);
	int k = rast / 2;
	if (l == 0)
	{
		dc.Rectangle(minixwerh+k, miniywerh-ky, minixwerh + k + kx, miniywerh);
		dc.SelectObject(pOldBrush);	mybrush.DeleteObject();
		return minixwerh + k;
	}
	else
	{
		dc.Rectangle(minixwerh - k, miniywerh - ky, minixwerh - k + kx, miniywerh);
		dc.SelectObject(pOldBrush);	mybrush.DeleteObject();
		return minixwerh - k;
	}
}

void CMFCmyProectDlg::OnAbout()
{
	CAboutDlg dlg;
	dlg.DoModal();
}


void CMFCmyProectDlg::OnBaschnjaPrawila()
{
	CBaschnjaDlg dlg;
	dlg.DoModal();

}


void CMFCmyProectDlg::Thor()
{
	CMenu* pMenu = GetMenu();
	pMenu->EnableMenuItem(ID_BASCHNJA, MF_GRAYED);
	pMenu->EnableMenuItem(ID_FEANOR_L, MF_GRAYED);
	pMenu->EnableMenuItem(ID_FEANOR_S, MF_GRAYED);
	tim = 120;
	ifthor = 1;
	CClientDC dc(this);//один раз на функцию
	CBrush mybrush;
	CBrush* pOldBrush;
	HBITMAP hb;
	HDC hMemDC;
	CPen hpen;
	CPen* pOldPen;
	CFont MyFont;
	MSG mes;

	mybrush.CreateSolidBrush(RGB(255, 255, 255));//255 255 255 белый, 0 0 0 черный
	pOldBrush = dc.SelectObject(&mybrush);
	MoveWindow(0, 0, X, Y+10, TRUE);
	dc.Rectangle(0, 0, X, Y+10);
	dc.SelectObject(pOldBrush);//удаление кисточки (+ строка ниже)
	mybrush.DeleteObject();
	
	int sir_jotun;
	if (Y / 7 > 115) sir_jotun = 115;
	else sir_jotun = Y / 7;
	for (int i = 0;i < 6;i++)
	{
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_JOTUN));
		hMemDC = ::CreateCompatibleDC(NULL);
		SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC,Y/30+ i*115, 0, sir_jotun, sir_jotun,//адресат-экран
			hMemDC, 0, 0, 800, 800, SRCCOPY); //источник
			::DeleteDC(hMemDC);
		::DeleteObject(hb);
	}
	//стена 
	hpen.CreatePen(PS_SOLID, 3, RGB(0, 0, 0));
	pOldPen = dc.SelectObject(&hpen);
	mybrush.CreateSolidBrush(RGB(112,146, 190));
	pOldBrush = dc.SelectObject(&mybrush);
	int i=0,j,d = Y / 30;
	//горизонталь
	while (i < 115 * 6 + d * 3)
	{
		dc.Rectangle(i, sir_jotun, i+d*2, sir_jotun +d);
		i += d * 2;
	}
	j = sir_jotun + d;
	i -= d;
	//вертикаль
	while (j < Y)
	{
		dc.Rectangle(i, j, i + d, j + d * 2);
		dc.Rectangle(0, j, d, j + d * 2);
		j += d * 2;
	}

	//размеры торыча
	double Kspina, Kbok;
	int tSpina, tBok,rost;
	Kspina = 322 / 115.0; Kbok=258/115.0;
	if (Y / 4 < 258) { tSpina = Y / 4 / Kspina; tBok = Y / 4 / Kbok; rost = Y / 4; }
	else { tSpina = 258 / Kspina; tBok = 115; rost = 258; }
	
	
	hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_THOR_RIGHT));
	hMemDC = ::CreateCompatibleDC(NULL);
	SelectObject(hMemDC, hb);
	::StretchBlt(dc.m_hDC, 2 * 115, Y - rost-50, tBok, rost,//адресат-экран
		hMemDC, 0, 0, 115, 258, SRCCOPY); //источник
		::DeleteDC(hMemDC);
		::DeleteObject(hb);

	//mjolnirs
	for (int f = 0;f < 3;f++)
	{
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_MJOLNIR));
		hMemDC = ::CreateCompatibleDC(NULL);
		SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, X - (X - 115 * 6 + 2 * d) / 2 + 40*f, sir_jotun, 40, 61, hMemDC, 0, 0, 40, 61, SRCCOPY);
		::DeleteDC(hMemDC);
		::DeleteObject(hb);
	}
	//
	hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_TIME));
	hMemDC = ::CreateCompatibleDC(NULL);
	SelectObject(hMemDC, hb);
	::StretchBlt(dc.m_hDC, X - (X - 115 * 6 + 2 * d) / 2 -95, Y/2-90, 191, 191, hMemDC, 0, 0, 191, 191, SRCCOPY);
	::DeleteDC(hMemDC);
		::DeleteObject(hb);
	dc.SetBkMode(TRANSPARENT);
	MyFont.CreateFont(28, 0, 0, 0, 700, FALSE, FALSE, 0, ANSI_CHARSET,
		OUT_DEFAULT_PRECIS, CLIP_DEFAULT_PRECIS,
		DEFAULT_QUALITY, DEFAULT_PITCH | FF_SWISS,
		L"Old English Text MT");
	dc.SelectObject(&MyFont);
	dc.SetTextColor(RGB(0, 0, 0));
	dc.TextOut(X - (X - 115 * 6 + 2 * d) / 2 - 25, Y / 2,  L"2:00");
	dc.SelectObject(pOldBrush);//удаление кисточки (+ строка ниже)
	mybrush.DeleteObject();
		mybrush.CreateSolidBrush(RGB(255, 255, 255));
		pOldBrush = dc.SelectObject(&mybrush);
	bool Smert=0;
	i = Sl-1;
	int kolMjo = 3;
	int xkrug[100];
	int ykrug[100];
	int kolkrug = 0, dorogka;
	int x = 2 * 115;//координаты торыча в данный момент слева
	////////////
	SetTimer(1, 1000, NULL);
	/////////
	while (tim>0)
	{
		if (Smert) break;
		i++;
		if (PeekMessage(&mes, NULL, 0, 0, PM_REMOVE))
		{
			TranslateMessage(&mes);
			DispatchMessage(&mes);
		}
		
		//Thors Bewegung
		if (r == 1)
		{
			r = 0;
			dc.SelectObject(pOldPen);hpen.DeleteObject();
			hpen.CreatePen(PS_SOLID, 10, RGB(255,255, 255));
			pOldPen = dc.SelectObject(&hpen);
			dc.MoveTo(x+5, Y - rost - 50);
			dc.LineTo(x + 5, Y - 50);
			if (x <= 115 * 6 - 10 - d)
				x += 10;
			hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_THOR_RIGHT));
			hMemDC = ::CreateCompatibleDC(NULL);
			SelectObject(hMemDC, hb);
			::StretchBlt(dc.m_hDC, x, Y - rost - 50, tBok, rost,//адресат-экран
				hMemDC, 0, 0, 115, 258, SRCCOPY); //источник
				::DeleteDC(hMemDC);
		::DeleteObject(hb);
		}
		if (l == 1)
		{
			l = 0;
			dc.SelectObject(pOldPen);hpen.DeleteObject();
			hpen.CreatePen(PS_SOLID, 10, RGB(255, 255, 255));
			pOldPen = dc.SelectObject(&hpen);
			dc.MoveTo(x +tBok-5, Y - rost - 50);
			dc.LineTo(x +tBok- 5, Y - 50);
			if (x >= d + 10)
				x -= 10;
			hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_THOR_LEFT));
			hMemDC = ::CreateCompatibleDC(NULL);
			SelectObject(hMemDC, hb);
			::StretchBlt(dc.m_hDC, x, Y - rost - 50, tBok, rost,//адресат-экран
				hMemDC, 0, 0, 115, 258, SRCCOPY); //источник
				::DeleteDC(hMemDC);
		::DeleteObject(hb);
		}
        dc.SelectObject(pOldPen);hpen.DeleteObject();dc.SelectObject(pOldBrush); mybrush.DeleteObject();
		hpen.CreatePen(PS_SOLID, 3, RGB(32, 72, 204));
		pOldPen = dc.SelectObject(&hpen);
		mybrush.CreateSolidBrush(RGB(153,217 ,234 ));
		pOldBrush = dc.SelectObject(&mybrush);
		
		if (i==Sl)//новый шарик
		{
			i =1;
		dorogka = (rand()) % 6 ;
		xkrug[kolkrug] = dorogka * 115 + d + 40;
		ykrug[kolkrug] = sir_jotun + d +40;
		kolkrug++;
		}
		for (int j=0;j<kolkrug;j++)
		{ 
		dc.Ellipse(xkrug[j]-35, ykrug[j]-35, xkrug[j]+35, ykrug[j]+35);
		dc.ExtFloodFill(xkrug[j], ykrug[j], RGB(32, 72, 204), FLOODFILLBORDER);
		}
		Sleep(Sk);
		if (Mjo==1)
		{
			Mjo = 0;
			if (kolMjo != 0)
			{
				
				dc.SelectObject(pOldPen);hpen.DeleteObject();dc.SelectObject(pOldBrush); mybrush.DeleteObject();
				hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
				pOldPen = dc.SelectObject(&hpen);
				mybrush.CreateSolidBrush(RGB(255, 255, 255));
				pOldBrush = dc.SelectObject(&mybrush);
				dc.Rectangle(x, Y - rost - 50, x + tBok, Y + 10);
				dc.Rectangle(X - (X - 115 * 6 + 2 * d) / 2 + 40 * (kolMjo-1), sir_jotun, X - (X - 115 * 6 + 2 * d) / 2 + 40 * kolMjo+40, sir_jotun+61);
				kolMjo--;
				//вывод тора со спины
	hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_THOR_SPINA));
	hMemDC = ::CreateCompatibleDC(NULL);
	SelectObject(hMemDC, hb);
	::StretchBlt(dc.m_hDC, x, Y-rost-50, tSpina, rost,//адресат-экран
		hMemDC, 0, 0, 115, 322, SRCCOPY); 
		::DeleteDC(hMemDC);
		::DeleteObject(hb);

				
			//wwerh mjolnir
				for (int j = Y - rost - 50 - 61;j > sir_jotun + d + 10;j -= 3)
				{
					dc.SelectObject(pOldPen);hpen.DeleteObject();
					hpen.CreatePen(PS_SOLID, 3, RGB(0, 162, 232));
					pOldPen = dc.SelectObject(&hpen);
					hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_MJOLNIR));
					hMemDC = ::CreateCompatibleDC(NULL);
					SelectObject(hMemDC, hb);
					::StretchBlt(dc.m_hDC, x + tSpina / 2 - 20, j,40, 61,//адресат-экран
						hMemDC, 0, 0, 40, 61, SRCCOPY); //источник
						::DeleteDC(hMemDC);
		::DeleteObject(hb);
					dc.Ellipse(x, j - 10, x + tBok, j);
					Sleep(8);
					dc.SelectObject(pOldPen);hpen.DeleteObject();
					hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
					pOldPen = dc.SelectObject(&hpen);
					dc.Rectangle(x-2, j-10, x + tBok+2,j+61);

				}
				dc.SelectObject(pOldPen);hpen.DeleteObject();
				hpen.CreatePen(PS_SOLID, 3, RGB(0, 162, 232));
				pOldPen = dc.SelectObject(&hpen);
				dc.MoveTo(x, sir_jotun+d+1);
				dc.LineTo(x+ tBok, sir_jotun + d + 1);
				hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_MJOLNIR));
				hMemDC = ::CreateCompatibleDC(NULL);
				SelectObject(hMemDC, hb);
				::StretchBlt(dc.m_hDC, x + tSpina / 2 - 20, sir_jotun + d + 4, 40, 61,	hMemDC, 0, 0, 40, 61, SRCCOPY);
				::DeleteDC(hMemDC);
		::DeleteObject(hb);
				dc.MoveTo(x, sir_jotun + d + 31);
				dc.LineTo(x + tBok /2, sir_jotun + d + 1);
				dc.LineTo(x + tBok, sir_jotun + d + 31);
				dc.MoveTo(x, sir_jotun + d + 61);
				dc.LineTo(x + tBok / 2, sir_jotun + d + 1);
				dc.LineTo(x + tBok, sir_jotun + d + 61);
				///////////////////////////////////////////////////////////уничтожение глыб
				dc.SelectObject(pOldPen);hpen.DeleteObject();
				hpen.CreatePen(PS_SOLID, 2, RGB(255, 255, 255));
				pOldPen = dc.SelectObject(&hpen);
				for (int u = 0;u < kolkrug;)
				{
					if (((xkrug[u] + 35 >= x) && (xkrug[u] +35 <= x+tBok)) || ((xkrug[u] - 35 >= x) && (xkrug[u] - 35 <= x + tBok)))
					{
						for (int kr = 0;kr <= 36;kr++)
						{
							dc.Ellipse(xkrug[u]-kr, ykrug[u]-kr, xkrug[u] + kr, ykrug[u] +kr);
							Sleep(3);
						}
						kolkrug--;
						for (int j = u;j < kolkrug;j++)
						{
							ykrug[j] = ykrug[j + 1];
							xkrug[j] = xkrug[j + 1];
						}
						ykrug[kolkrug] = NULL;
						xkrug[kolkrug] = NULL;
						u--;
					}
					u++;
				}
				//////wniz mjolnir
				dc.Rectangle(x, sir_jotun+d+1, x + tBok+2, sir_jotun + d  + 65);
				for (int j =sir_jotun + d + 3 ;j >Y - rost - 50 - 61*2 ;j += 2)
				{					
					hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_MJOLNIR));
					hMemDC = ::CreateCompatibleDC(NULL);
					SelectObject(hMemDC, hb);
					::StretchBlt(dc.m_hDC, x + tSpina / 2 - 20, j, 40, 61,//адресат-экран
						hMemDC, 0, 0, 40, 61, SRCCOPY); //источник
						::DeleteDC(hMemDC);
		::DeleteObject(hb);
					Sleep(8);
					dc.MoveTo(x, j);
					dc.LineTo(x + tBok, j);	
				}
				int s = 0;
				for (int j = x + tSpina / 2 - 20;j < x + tSpina- 40;j += 1)
				{
					hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_MJOLNIR));
					hMemDC = ::CreateCompatibleDC(NULL);
					SelectObject(hMemDC, hb);
					::StretchBlt(dc.m_hDC, j, Y - rost - 50 - 61 * 2 +s, 40, 61,//адресат-экран
						hMemDC, 0, 0, 40, 61, SRCCOPY); //источник
						::DeleteDC(hMemDC);
		::DeleteObject(hb);
					Sleep(8);
					dc.MoveTo(j, Y - rost - 50 - 61 * 2 + s);
					dc.LineTo(j + tSpina-s/2, Y - rost - 50 - 61 * 2 + s);
					dc.MoveTo(j, Y - rost - 50 - 61 * 2 + s);
					dc.LineTo(j, Y - rost - 50 - 61 * 2 + s + 61);
					s += 2;
				}
				s -= 2;
				for (int j = Y - rost - 50 - 61 * 2 + s;j < Y-rost-50-61;j +=2)
				{
					hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_MJOLNIR));
					hMemDC = ::CreateCompatibleDC(NULL);
					SelectObject(hMemDC, hb);
					::StretchBlt(dc.m_hDC, x + tSpina - 40, j, 40, 61,//адресат-экран
						hMemDC, 0, 0, 40, 61, SRCCOPY); //источник
						::DeleteDC(hMemDC);
		::DeleteObject(hb);
					Sleep(8);
					dc.MoveTo(x + tSpina - 40, j);
					dc.LineTo(x + tSpina, j);
					
				}
				dc.Rectangle(x + tSpina - 40, Y - rost - 50-61, x + tSpina, Y - rost - 50);
				/////////////////////////////
				hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_THOR_RIGHT));
				hMemDC = ::CreateCompatibleDC(NULL);
				SelectObject(hMemDC, hb);
				::StretchBlt(dc.m_hDC, x, Y - rost - 50, tBok, rost,//адресат-экран
					hMemDC, 0, 0, 115, 258, SRCCOPY); //источник
					::DeleteDC(hMemDC);
		::DeleteObject(hb);
			}
		}
			   
		dc.SelectObject(pOldPen);hpen.DeleteObject();dc.SelectObject(pOldBrush); mybrush.DeleteObject();
		hpen.CreatePen(PS_SOLID, 3, RGB(255, 255, 255));
		pOldPen = dc.SelectObject(&hpen);
		mybrush.CreateSolidBrush(RGB(255, 255, 255));
		pOldBrush = dc.SelectObject(&mybrush);
		for (int j = 0;j < kolkrug;j++)
		{
			dc.ExtFloodFill(xkrug[j], ykrug[j], RGB(32, 72, 204), FLOODFILLBORDER);
			dc.Ellipse(xkrug[j] - 35, ykrug[j] - 35, xkrug[j] + 35, ykrug[j] + 35);
		}
		for (int j = 0;j < kolkrug;j++)
		{
			ykrug[j] += 3;
		}
		if (ykrug[0]>=Y+10)
		{	
			kolkrug--;		
			for (int j = 0;j < kolkrug;j++)
			{
				ykrug[j] = ykrug[j+1];
				xkrug[j]=xkrug[j+1];
			}
			ykrug[kolkrug] =NULL;
			xkrug[kolkrug] = NULL;
          
		}
		
		for (int u = 0;u < kolkrug;u++)
		{
			if (((xkrug[u] + 35 >= x) && (xkrug[u] + 35 <= x + tBok)) || ((xkrug[u] - 35 >= x) && (xkrug[u] - 35 <= x + tBok)))
				if (ykrug[u] >= Y - rost - 50)
					Smert = 1;
		}
		
	}
	//////
	KillTimer(1);
	///////
	if (Smert == 1)
	{
		dc.SelectObject(pOldBrush);
		mybrush.DeleteObject();
		mybrush.CreateSolidBrush(RGB(0, 0, 0));
		pOldBrush = dc.SelectObject(&mybrush);
		dc.Rectangle(0, 0, X,Y+10);
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_KILL_THOR));
		hMemDC = ::CreateCompatibleDC(NULL);
		SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, X/2-1344/2, Y+10-559, 1344, 559,//адресат-экран
			hMemDC, 0, 0, 1344,559, SRCCOPY); //источник
			::DeleteDC(hMemDC);
		::DeleteObject(hb);
		dc.SetBkMode(TRANSPARENT);
		MyFont.CreateFont(Y / 7, 0, 0, 0, 700, FALSE, FALSE, 0, ANSI_CHARSET,
			OUT_DEFAULT_PRECIS, CLIP_DEFAULT_PRECIS,
			DEFAULT_QUALITY, DEFAULT_PITCH | FF_SWISS,
			L"Arial");
		dc.SelectObject(&MyFont);
		dc.SetTextColor(RGB(168, 0, 0));
		dc.TextOut(X / 2 - (Y/7)*3, 10, L"ВЫ ПРОИГРАЛИ...");
	}
	else
	{
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_BIWRIOST));
		hMemDC = ::CreateCompatibleDC(NULL);
		SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, x, Y -rost-50-tBok, tBok, tBok,//адресат-экран
			hMemDC, 0, 0, 115, 115, SRCCOPY); //источник
			::DeleteDC(hMemDC);
		::DeleteObject(hb);
		Sleep(2000);
		//////////////////////////////вывод пира в Асгарде
		dc.SelectObject(pOldBrush);
		mybrush.DeleteObject();
		mybrush.CreateSolidBrush(RGB(206,174,226));//крч фон картинки
		pOldBrush = dc.SelectObject(&mybrush);
		dc.Rectangle(0, 0, X, Y + 10);
		dc.SetBkMode(TRANSPARENT);
		MyFont.CreateFont(Y / 10, 0, 0, 0, 700, FALSE, FALSE, 0, ANSI_CHARSET,
			OUT_DEFAULT_PRECIS, CLIP_DEFAULT_PRECIS,
			DEFAULT_QUALITY, DEFAULT_PITCH | FF_SWISS,
			L"Arial");
		dc.SelectObject(&MyFont);
		dc.SetTextColor(RGB(128, 0, 255));//типа щас фиголетовый, но надо подобрать
		//сама картинка
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_PIR));
		hMemDC = ::CreateCompatibleDC(NULL);
		SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC,X/2-632 , (Y-10-Y/10-558)/2+10+Y/10, 1265, 558,//адресат-экран
			hMemDC, 0, 0, 1265, 558, SRCCOPY);
			::DeleteDC(hMemDC);
		::DeleteObject(hb);
		dc.TextOut(X / 2 - 330, 10, L"!!ПОБЕДА!!");
	}

ifthor = 0;
	::DeleteDC(hMemDC);
	::DeleteObject(hb);
	dc.SelectObject(pOldPen);hpen.DeleteObject();dc.SelectObject(pOldBrush); mybrush.DeleteObject();
	pMenu->EnableMenuItem(ID_BASCHNJA, MF_ENABLED);
	pMenu->EnableMenuItem(ID_FEANOR_L, MF_ENABLED);
	pMenu->EnableMenuItem(ID_FEANOR_S, MF_ENABLED);
}


void CMFCmyProectDlg::OnThorL()
{
	Sl = 200;
	Sk =10;
	Thor();
}


void CMFCmyProectDlg::OnThorSr()
{
	Sl = 100;
	Sk = 10;
	Thor();
}


void CMFCmyProectDlg::OnThorSl()
{
	Sl = 50;
	Sk = 10;
	Thor();
}


void CMFCmyProectDlg::OnTimer(UINT_PTR nIDEvent)
{
	CClientDC dc(this);//один раз на функцию
	CBrush mybrush;
	CBrush* pOldBrush;
	CFont MyFont;
	TCHAR s[5];
	CPen hpen;
	CPen* pOldPen;

	tim--;
	s[0] = tim / 60 +48;
	s[1] = ':';
	s[2] = (tim % 60) / 10 + 48;
	s[3] = (tim % 60) % 10 + 48;
	s[4] = '\0';
	if (ifthor == 1)
	{
		hpen.CreatePen(PS_SOLID, 3, RGB(239, 228, 176));
		pOldPen = dc.SelectObject(&hpen);
		mybrush.CreateSolidBrush(RGB(239, 228, 176));
		pOldBrush = dc.SelectObject(&mybrush);
		dc.Rectangle(X - (X - 115 * 6 + 2 * Y / 30) / 2 - 25, Y / 2, X - (X - 115 * 6 + 2 * Y / 30) / 2 + 28, Y / 2 + 30);
		dc.SetBkMode(TRANSPARENT);
		MyFont.CreateFont(28, 0, 0, 0, 700, FALSE, FALSE, 0, ANSI_CHARSET,
			OUT_DEFAULT_PRECIS, CLIP_DEFAULT_PRECIS,
			DEFAULT_QUALITY, DEFAULT_PITCH | FF_SWISS,
			L"Old English Text MT");
		dc.SelectObject(&MyFont);
		dc.SetTextColor(RGB(0, 0, 0));
		dc.TextOut(X - (X - 115 * 6 + 2 * Y / 30) / 2 - 25, Y / 2, s);
		dc.SelectObject(pOldBrush);	mybrush.DeleteObject();
		dc.SelectObject(pOldPen); hpen.DeleteObject();
		CDialogEx::OnTimer(nIDEvent);
	}
	if ((iffea==1)&&(iffea2==0))
	{
		hpen.CreatePen(PS_SOLID, 3, RGB(239, 228, 176));
		pOldPen = dc.SelectObject(&hpen);
		mybrush.CreateSolidBrush(RGB(239, 228, 176));
		pOldBrush = dc.SelectObject(&mybrush);
		dc.Rectangle(X/ 2 - 25, 95, X / 2+28,95 + 30);
		dc.SetBkMode(TRANSPARENT);
		MyFont.CreateFont(28, 0, 0, 0, 700, FALSE, FALSE, 0, ANSI_CHARSET,
			OUT_DEFAULT_PRECIS, CLIP_DEFAULT_PRECIS,
			DEFAULT_QUALITY, DEFAULT_PITCH | FF_SWISS,
			L"Old English Text MT");
		dc.SelectObject(&MyFont);
		dc.SetTextColor(RGB(0, 0, 0));
		dc.TextOut(X / 2 - 25, 95, s);
		dc.SelectObject(pOldBrush);	mybrush.DeleteObject();
		dc.SelectObject(pOldPen); hpen.DeleteObject();
		CDialogEx::OnTimer(nIDEvent);
	}
	if(iffea2==1)
		CDialogEx::OnTimer(nIDEvent);

}


void CMFCmyProectDlg::OnThorPravila()
{
	CThorPrawDlg dlg;
	dlg.DoModal();
}


void CMFCmyProectDlg::OnFeanorL()
{
	Feanor(7);
}


void CMFCmyProectDlg::OnFeanorS()
{
	Feanor(8);
}


void CMFCmyProectDlg::OnFeanorPr()
{
	CFeanorDlg dlg;
	dlg.DoModal();
}

void CMFCmyProectDlg::Feanor(int vM)
{
	CMenu* pMenu = GetMenu();
	pMenu->EnableMenuItem(ID_BASCHNJA, MF_GRAYED);
	pMenu->EnableMenuItem(ID_THOR_L, MF_GRAYED);
	pMenu->EnableMenuItem(ID_THOR_SR, MF_GRAYED);
	pMenu->EnableMenuItem(ID_THOR_SL, MF_GRAYED);
	tim = 80;
	
	CClientDC dc(this);//один раз на функцию
	CBrush mybrush;
	CBrush* pOldBrush;
	HBITMAP hb;
	HDC hMemDC;
	CPen hpen;
	CPen* pOldPen;
	CFont MyFont;
	MSG mes;

	mybrush.CreateSolidBrush(RGB(255, 255, 255));//255 255 255 белый, 0 0 0 черный
	pOldBrush = dc.SelectObject(&mybrush);
	MoveWindow(0, 0, X, Y + 10, TRUE);
	dc.Rectangle(0, 0, X, Y + 10);
	dc.SelectObject(pOldBrush);//удаление кисточки (+ строка ниже)
	mybrush.DeleteObject();
	mybrush.CreateSolidBrush(RGB(116, 242, 55));	
	pOldBrush = dc.SelectObject(&mybrush);
	dc.Rectangle(0, Y*0.8, X, Y + 10);
	dc.SelectObject(pOldBrush);//удаление кисточки (+ строка ниже)
	mybrush.DeleteObject();

	///////////////////////////////////////   timer
	
	hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_TIME));
	
	hMemDC = ::CreateCompatibleDC(NULL);
	SelectObject(hMemDC, hb);
	::StretchBlt(dc.m_hDC, X/ 2 - 95, 5, 191, 191, hMemDC, 0, 0, 191, 191, SRCCOPY);
	::DeleteDC(hMemDC);
	::DeleteObject(hb);
	dc.SetBkMode(TRANSPARENT);
	MyFont.CreateFont(28, 0, 0, 0, 700, FALSE, FALSE, 0, ANSI_CHARSET,
		OUT_DEFAULT_PRECIS, CLIP_DEFAULT_PRECIS,
		DEFAULT_QUALITY, DEFAULT_PITCH | FF_SWISS,
		L"Old English Text MT");
	dc.SelectObject(&MyFont);
	dc.SetTextColor(RGB(0, 0, 0));
	dc.TextOut(X / 2 - 25, 95, L"1:20");
	dc.SelectObject(pOldBrush);//удаление кисточки (+ строка ниже)
	mybrush.DeleteObject();
	
	////////////	
	/////////////////////////
	
	//уменьшение картинок
	float kf = 0.5, km=0.45;
	/////
	int xm; xm = X - 5 - 602 * km;
	int x[2][3]; x[0][0] = X / 3; x[0][1] = X * 2 / 3; x[0][2] = X; x[1][0] = x[1][1] = x[1][2] = 2;
	int  vf1 =9,vf = vf1;
	iffea = 1;
	int up = 0,dog=0,sb=0;
	int kolw = 0,kold=0;
	int kolw1 = 180, kold1=200+210*kf+55;
	int xf = 100;
	int sle = 50;
	int z = 8;
	int i;
		//1000*75 * 7 /4 / (xm - xf - 342 * kf);
	int k = 0;
	////
	SetTimer(10, 1000, NULL);
	///////////////////////////////////////%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
	while (tim > 0)

	{
		if (PeekMessage(&mes, NULL, 0, 0, PM_REMOVE))
		{
			TranslateMessage(&mes);
			DispatchMessage(&mes);
		}
		//prig wwerh
		if (feapw == 1)
		{
			feapw = 0;
			if (kolw < 0) kolw = kolw1;
			vf = vf1;
		}
		//prig dlin
		if (feapd == 1)
		{
			feapd = 0;
			if ((kold < 0)&& (kolw< 0)) kold = kold1;
			vf = vf1;
		}
		//**************************************
		if ((kolw == 0)||(kold==0))
		{	
			mybrush.CreateSolidBrush(RGB(255, 255, 255));
			pOldBrush = dc.SelectObject(&mybrush);
			hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
			pOldPen = dc.SelectObject(&hpen);
			if(kolw==0) dc.Rectangle(xf, Y*0.8 - 625 * kf - 70, xf + 339 * kf, Y*0.8 - 70); kolw -= 5; vf = vf1;
			if (kold == 0) dc.Rectangle(xf, Y*0.8 - 588 * kf - 70, xf + 618 * kf, Y*0.8 - 70); kold -= 5; vf = vf1;
			dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
			//F_4 	
				hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_4));
				hMemDC = ::CreateCompatibleDC(NULL);
				SelectObject(hMemDC, hb);
				::StretchBlt(dc.m_hDC, xf, Y*0.8 - 650 * kf, 316 * kf, 650 * kf,//адресат-экран
					hMemDC, 0, 0, 316, 650, SRCCOPY);
				::DeleteDC(hMemDC);
				::DeleteObject(hb);			
		}
		
		if ((kolw == kolw1)||(kold==kold1))
		{ mybrush.CreateSolidBrush(RGB(255, 255, 255));
			pOldBrush = dc.SelectObject(&mybrush);
			hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
			pOldPen = dc.SelectObject(&hpen);
				dc.Rectangle(xf, Y*0.8 - 674 * kf, xf + 316 * kf, Y*0.8);
				dc.Rectangle(xf, Y*0.8 - 625 * kf - 70, xf + 618 * kf, Y*0.8 - 70);
			dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
			if (kolw == kolw1) feaprw_ris();
			if (kold == kold1) feaprd_ris();
		}
		//-----------------------------------------------------------------------------------
		if (k <= 0)
		{
			mybrush.CreateSolidBrush(RGB(255, 255, 255));
			pOldBrush = dc.SelectObject(&mybrush);
			hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
			pOldPen = dc.SelectObject(&hpen);
			if (vf > vM)
				dc.Rectangle(xm + 602 * km - vf, Y*0.8 - 760 * km, xm + 602 * km, Y*0.8);
			else
				dc.Rectangle(xm, Y*0.8 - 760 * km, xm + vM, Y*0.8);
			dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
			
			if (k == z*(-1))
				//-M_2
			{
				mybrush.CreateSolidBrush(RGB(255, 255, 255));
				pOldBrush = dc.SelectObject(&mybrush);
				hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
				pOldPen = dc.SelectObject(&hpen);
				dc.Rectangle(xm, Y*0.8 - 760 * km, xm + 602 * km, Y*0.8);
				dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
			}
			xm = xm - vf + vM;
			// M_1
			hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_M_1));
			hMemDC = ::CreateCompatibleDC(NULL);
			SelectObject(hMemDC, hb);
			::StretchBlt(dc.m_hDC, xm, Y*0.8 - 756 * km, 602 * km, 756 * km,//адресат-экран
				hMemDC, 0, 0, 602, 756, SRCCOPY);
			::DeleteDC(hMemDC);
			::DeleteObject(hb);
		}
			//-----------------------------------------------------------------------------------
			if (k == 0)
			{	//-F_3
				mybrush.CreateSolidBrush(RGB(255, 255, 255));
				pOldBrush = dc.SelectObject(&mybrush);
				hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
				pOldPen = dc.SelectObject(&hpen);
				if ((kolw < 0)&&(kold<0))
					dc.Rectangle(xf, Y*0.8 - 674 * kf, xf + 316 * kf, Y*0.8);
				dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
				//F_2 				
				if ((kolw < 0)&&(kold<0))
				{
					hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_2));
					hMemDC = ::CreateCompatibleDC(NULL);
					SelectObject(hMemDC, hb);
					::StretchBlt(dc.m_hDC, xf, Y*0.8 - 657 * kf, 312 * kf, 657 * kf,//адресат-экран
						hMemDC, 0, 0, 312, 657, SRCCOPY);
					::DeleteDC(hMemDC);
					::DeleteObject(hb);
				}
			}
		
		k++;
		///////////////////////////////////////////stop
		for (int i = 0; i < 3; i++)
		{
			if ((x[1][i]%2 == 1)&&  (kolw <=0) &&(x[0][i] - (xf + 340 * kf) >=0) && (x[0][i] - (xf + 340 * kf) <=vf1) ) vf = 0;
			/*if ((xf-x[0][i]>=0)&&(xf-x[0][i]<=90)&&(x[1][i]%2==1)&&(kolw<=0)) vf=0;*/
			if ( (x[1][i]%2 == 1)&&(kolw <=0) && ( x[0][i]-xf >= 0) && (xf + 340 * kf - x[0][i] >=0) ) vf = 0;
		}
		////////////////////////////
		///////////////////////////////////////////upal		
		for (i = 0; i < 3; i++)
		{
			if ((x[1][i] == 0) && (kold <= 0) && (kolw <= 0) && ((xf + 210 * kf) - x[0][i] >= 0) && (x[0][i] + 200 - (xf + 210 * kf) > 0)) { up = 1; break; }
			
			if ((x[1][i]  == 0) && (kold <= 0) && (kolw <= 0) && (xf+210*kf-x[0][i]-200 >= 0) && (x[0][i]+200-xf >= 0)) { up = 1; break; }
		}
		 if(up == 1) break; 
		////////////////////////////
		///////////////////////////////////////////sbegal
		if (xm > X) { sb = 1; break; }			
		////////////////////////////
		///////////////////////////////////////////dognal
		if (xm <= xf+316*kf) { dog = 1; break; }
		////////////////////////////
		//закрасить
		for (int i = 0; i < 3; i++)
		{
			if (x[1][i] == 0)
			{
				mybrush.CreateSolidBrush(RGB(116, 242, 55));
				pOldBrush = dc.SelectObject(&mybrush);
				hpen.CreatePen(PS_SOLID, 1, RGB(116, 242, 55));
				pOldPen = dc.SelectObject(&hpen);
				dc.Rectangle(x[0][i]+200-vf, Y*0.8, x[0][i] + 200, Y + 10);
				dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
			}
			if (x[1][i] % 2 == 1)
			{
				mybrush.CreateSolidBrush(RGB(255, 255, 255));
				pOldBrush = dc.SelectObject(&mybrush);
				hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
				pOldPen = dc.SelectObject(&hpen);
				dc.Rectangle(x[0][i]+70-vf, Y*0.8 - 50, x[0][i] + 70, Y *0.8);
				dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
			}
		}
		//
		for (int i = 0; i < 3; i++)
			x[0][i] -= vf;

		if (((x[0][0]+200 <= 0)&&(x[1][0]==0))||((x[0][0]+70<=0)&&(x[1][0]%2==1))||((x[0][0]<=0)&&(x[1][0]%2==0)&&(x[1][0]!=0)))
		{
			x[0][0] = x[0][1];
			x[0][1] = x[0][2];
			x[1][0] = x[1][1];
			x[1][1] = x[1][2];

			x[1][2] = (rand()) % 5;
			x[0][2] = X;
		}
		//нарисовать
		for (int i = 0; i < 3; i++)
		{
			if (x[1][i] == 0)
			{
				mybrush.CreateSolidBrush(RGB(255, 255, 255));
				pOldBrush = dc.SelectObject(&mybrush);
				hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
				pOldPen = dc.SelectObject(&hpen);
				dc.Rectangle(x[0][i], Y*0.8, x[0][i] + 200, Y + 10);
				dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
			}
			if (x[1][i] % 2 == 1)
			{
				mybrush.CreateSolidBrush(RGB(195, 195, 195));
				pOldBrush = dc.SelectObject(&mybrush);
				hpen.CreatePen(PS_SOLID, 1, RGB(116, 242, 55));
				pOldPen = dc.SelectObject(&hpen);
				dc.Rectangle(x[0][i], Y*0.8 - 50, x[0][i] + 70, Y *0.8);
				dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
			}
		}
		if (kolw > 0) kolw -= vf;
		if (kold > 0) kold -= vf;
		 Sleep(sle);
		//+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
		 if (k >= 0)
		 {			 
			 mybrush.CreateSolidBrush(RGB(255, 255, 255));
			 pOldBrush = dc.SelectObject(&mybrush);
			 hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
			 pOldPen = dc.SelectObject(&hpen);
			 if(vf>vM)
			 dc.Rectangle(xm+602 * km-vf, Y*0.8 - 760 * km, xm + 602 * km, Y*0.8);
			 else
				 dc.Rectangle(xm, Y*0.8 - 760 * km, xm +vM, Y*0.8);
			 dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
			
			 if(k==0)//-M_1;	
				 
			 {
				 mybrush.CreateSolidBrush(RGB(255, 255, 255));
				 pOldBrush = dc.SelectObject(&mybrush);
				 hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
				 pOldPen = dc.SelectObject(&hpen);
				 dc.Rectangle(xm, Y*0.8 - 760 * km, xm + 602 * km, Y*0.8);
				 dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
			 }
			 xm = xm - vf + vM;
			 // M_2
			 hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_M_2));
			 hMemDC = ::CreateCompatibleDC(NULL);
			 SelectObject(hMemDC, hb);
			 ::StretchBlt(dc.m_hDC, xm, Y*0.8 - 756 * km, 602 * km, 756 * km,//адресат-экран
				 hMemDC, 0, 0, 602, 737, SRCCOPY);
			 ::DeleteDC(hMemDC);
			 ::DeleteObject(hb);
		 }
		 
		if (k == z)
		{
			k = z*(-1);
			//-F_2 
			mybrush.CreateSolidBrush(RGB(255, 255, 255));
			pOldBrush = dc.SelectObject(&mybrush);
			hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
			pOldPen = dc.SelectObject(&hpen);
			if ((kolw < 0)&&(kold<0)) dc.Rectangle(xf, Y*0.8 - 657 * kf, xf + 312 * kf, Y*0.8);
					
			dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
			//F_3
			
			if ((kolw < 0)&&(kold<0))
			{
				hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_3));
				hMemDC = ::CreateCompatibleDC(NULL);
				SelectObject(hMemDC, hb);
				::StretchBlt(dc.m_hDC, xf, Y*0.8 - 674 * kf, 316 * kf, 674 * kf,//адресат-экран
					hMemDC, 0, 0, 316, 674, SRCCOPY);
				::DeleteDC(hMemDC);
				::DeleteObject(hb);
			}

			

		}
	}

    KillTimer(10);
	//////////////  Упал   ////////////////////////
	if (up == 1)
	{
		mybrush.CreateSolidBrush(RGB(255, 255, 255));
		pOldBrush = dc.SelectObject(&mybrush);
		hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
		pOldPen = dc.SelectObject(&hpen);		
		dc.Rectangle(xf, Y*0.8 - 625 * kf - 70, xf + 618 * kf, Y*0.8);
		int yf = Y * 0.8 - 714 * kf; k = 0;
		while (yf+k < Y + 10)
		{
			hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_PAD));
			hMemDC = ::CreateCompatibleDC(NULL);
			SelectObject(hMemDC, hb);
			::StretchBlt(dc.m_hDC, x[0][i]+200-300*kf-10, yf+k, 300 * kf, 714 * kf,//адресат-экран
				hMemDC, 0, 0, 300, 714, SRCCOPY);
			::DeleteDC(hMemDC);
			::DeleteObject(hb);
			k += 5;
			Sleep(45);
			dc.Rectangle(x[0][i] + 200 - 300 * kf - 10, yf + k-5, x[0][i]+200, yf+k);
		}
		dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
		mybrush.CreateSolidBrush(RGB(0, 0, 0));
		pOldBrush = dc.SelectObject(&mybrush);
		hpen.CreatePen(PS_SOLID, 1, RGB(0, 0, 0));
		pOldPen = dc.SelectObject(&hpen);
		dc.Rectangle(0, 0, X, Y+10);
		dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_K_MEL));
		hMemDC = ::CreateCompatibleDC(NULL);
		SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC,X/2-424*1.5/2,Y/2-291*1.5/2, 424*1.5, 291*1.5,//адресат-экран
			hMemDC, 0, 0, 424, 291, SRCCOPY);
		::DeleteDC(hMemDC);
		::DeleteObject(hb);
		dc.SetBkMode(TRANSPARENT);
		MyFont.CreateFont(Y / 7, 0, 0, 0, 700, FALSE, FALSE, 0, ANSI_CHARSET,
			OUT_DEFAULT_PRECIS, CLIP_DEFAULT_PRECIS,
			DEFAULT_QUALITY, DEFAULT_PITCH | FF_SWISS,
			L"Complex");
		dc.SelectObject(&MyFont);
		dc.SetTextColor(RGB(168, 0, 0));
		dc.TextOut(X / 2 - (Y / 7) * 3, 10, L"ВЫ ПРОИГРАЛИ...");
	}
	/*dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();*/
	if (sb == 1)  //сбежал
	{
		mybrush.CreateSolidBrush(RGB(255, 255, 255));
		pOldBrush = dc.SelectObject(&mybrush);
		hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
		pOldPen = dc.SelectObject(&hpen);
		dc.Rectangle(0, 0, X, Y*0.8);
		
			hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_F1));
			hMemDC = ::CreateCompatibleDC(NULL);
			SelectObject(hMemDC, hb);
			::StretchBlt(dc.m_hDC, xf, Y*0.8-702*0.7, 672*0.7, 702*0.7,//адресат-экран
				hMemDC, 0, 0, 672, 702, SRCCOPY);
			::DeleteDC(hMemDC);
			::DeleteObject(hb);			
		
		dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
		dc.SetBkMode(TRANSPARENT);
		MyFont.CreateFont(Y / 7, 0, 0, 0, 700, FALSE, FALSE, 0, ANSI_CHARSET,
			OUT_DEFAULT_PRECIS, CLIP_DEFAULT_PRECIS,
			DEFAULT_QUALITY, DEFAULT_PITCH | FF_SWISS,
			L"Complex");
		dc.SelectObject(&MyFont);
		dc.SetTextColor(RGB(168, 0, 0));
		dc.TextOut(X / 2 - (Y / 7) * 3, 10, L"ВЫ ПРОИГРАЛИ...");
	}
	if (dog == 1)
	{
		mybrush.CreateSolidBrush(RGB(255, 255, 255));
		pOldBrush = dc.SelectObject(&mybrush);
		hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));
		pOldPen = dc.SelectObject(&hpen);
		dc.Rectangle(0, 0, X, Y*0.8);

//F2
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_2));
		hMemDC = ::CreateCompatibleDC(NULL);
		SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, xf, Y*0.8 - 657 * 0.7, 312 * 0.7, 657 * 0.7,//адресат-экран
			hMemDC, 0, 0, 312,657, SRCCOPY);
		::DeleteDC(hMemDC);
		::DeleteObject(hb);
		// M_2
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_M_2));
		hMemDC = ::CreateCompatibleDC(NULL);
		SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, xf+524*0.7, Y*0.8 - 756 * 0.65, 602 * 0.65, 756 * 0.65,//адресат-экран
			hMemDC, 0, 0, 602, 737, SRCCOPY);
		::DeleteDC(hMemDC);
		::DeleteObject(hb);
		Sleep(1500);
		dc.Rectangle(0, 0, X, Y*0.8);
		//F_K_1
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_1));
		hMemDC = ::CreateCompatibleDC(NULL);
		SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, xf+20, Y*0.8 - 662 * 0.7, 524 * 0.7, 662 * 0.7,//адресат-экран
			hMemDC, 0, 0, 524, 662, SRCCOPY);
		::DeleteDC(hMemDC);
		::DeleteObject(hb);
		// M_1
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_M_1));
		hMemDC = ::CreateCompatibleDC(NULL);
		SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, xf + 524 * 0.7+20, Y*0.8 - 756 * 0.65, 602 * 0.65, 756 * 0.65,//адресат-экран
			hMemDC, 0, 0, 602, 756, SRCCOPY);
		::DeleteDC(hMemDC);
		::DeleteObject(hb);
		Sleep(1500);

		dc.Rectangle(0, 0, X, Y*0.8);
		//F_K_2
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_2));
		hMemDC = ::CreateCompatibleDC(NULL);
		SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, xf + 40, Y*0.8 - 590*0.7, 672*0.7, 702*0.7,//адресат-экран
			hMemDC, 0, 0, 672, 702, SRCCOPY);
		::DeleteDC(hMemDC);
		::DeleteObject(hb);
		Sleep(2000);

		dc.Rectangle(0, 0, X, Y*0.8);
		dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
		mybrush.CreateSolidBrush(RGB(116, 242, 55));
		pOldBrush = dc.SelectObject(&mybrush);
		hpen.CreatePen(PS_SOLID, 3, RGB(0, 64, 0));
		pOldPen = dc.SelectObject(&hpen);
		dc.Rectangle(0, 630*0.7-5,X, Y+10);
		dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
		//F_K_2
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_3));
		hMemDC = ::CreateCompatibleDC(NULL);
		SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, 0, 0, 1608 * 0.7, 920 * 0.7,//адресат-экран
			hMemDC, 0, 0,1608, 920, SRCCOPY);
		::DeleteDC(hMemDC);
		::DeleteObject(hb);
		
	}
	//555555555555555555555   Время вышло, не догнал   555555555555555555555555555555555555555555555555555555555555555555555555555555555555
	if (tim <= 0)
	{
		mybrush.CreateSolidBrush(RGB(255, 255, 255));pOldBrush = dc.SelectObject(&mybrush);
		hpen.CreatePen(PS_SOLID, 1, RGB(255, 255, 255));	pOldPen = dc.SelectObject(&hpen);
		dc.Rectangle(0, 0, X, Y + 10);
		
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_ZAM));
		hMemDC = ::CreateCompatibleDC(NULL); SelectObject(hMemDC, hb);
		double koef_zam;
		koef_zam=Y*1./1062;
		int tx = (int)((X-16) - 1220 * koef_zam);
		int sir = (int)(1220 * koef_zam);
		int dln = (int)(1062 * koef_zam);
		//::StretchBlt(dc.m_hDC, X-1220*0.7, Y+10-1062*0.7, 1220*0.7, 1062 * 0.7,	hMemDC, 0, 0, 1220, 1062, SRCCOPY);
		::StretchBlt(dc.m_hDC, tx, 0, sir, dln, hMemDC, 0, 0, 1220, 1062, SRCCOPY);
		::DeleteDC(hMemDC);	::DeleteObject(hb);

		/*TCHAR s[80];
		swprintf_s(s, L"X=%d  tx=%d, Y=%d %dx%d",  X, tx, Y, sir,dln);
		MessageBox(s, L"ZAMOK", MB_OK);*/

		k = 0; xm = 0; km = 0.25; int zd=50;
		while (xm+602*km < X-433*koef_zam-8)//while (xm < X-790*0.7) 433- ширина замка в bmp
		{// M_1
			hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_M_1));
			hMemDC = ::CreateCompatibleDC(NULL); SelectObject(hMemDC, hb);
			::StretchBlt(dc.m_hDC, xm, (int)(Y-756*km-zd), (int)(602 * km), (int)(756 * km), hMemDC, 0, 0, 602, 756, SRCCOPY);
			::DeleteDC(hMemDC);	::DeleteObject(hb);
			Sleep(50);
			
			dc.Rectangle(xm, (int)(Y - 756 * km -zd), xm+10, Y);
			xm += 10;
			// M_2
			/*hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_M_1));
			hMemDC = ::CreateCompatibleDC(NULL); SelectObject(hMemDC, hb);
			::StretchBlt(dc.m_hDC, xm, Y - 756 * km-zd, 602 * km, 756 * km, hMemDC, 0, 0, 602, 737, SRCCOPY);
			::DeleteDC(hMemDC);	::DeleteObject(hb);
			Sleep(50);
			dc.Rectangle(xm, Y - 756 * km -zd, xm + 10, Y);
			xm += 10;*/
		}
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_ZAM)); 
		hMemDC = ::CreateCompatibleDC(NULL); SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, tx, 0, sir, dln, hMemDC, 0, 0, 1220, 1062, SRCCOPY);
		::DeleteDC(hMemDC);	::DeleteObject(hb);
	///////////////////////////Timer<<<<<<<<<<<<<<<<<<<<<<<
		iffea2 = 1; tim = 2;
		SetTimer(2, 1000, NULL);		
		while (tim > 0) {
			if (PeekMessage(&mes, NULL, 0, 0, PM_REMOVE))
			{
				TranslateMessage(&mes);
				DispatchMessage(&mes);
			}
		}
		KillTimer(2);
		/////////////////////////
		
		xf = 0; km = 0.3;
		while (xf+312*km < X-sir)
		{// F_2
			hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_2));
			hMemDC = ::CreateCompatibleDC(NULL); SelectObject(hMemDC, hb);
			::StretchBlt(dc.m_hDC, xf, (int)(Y - 657 * km-zd), (int)(312 * km), (int)(657 * km), hMemDC, 0, 0, 312, 657, SRCCOPY);
			::DeleteDC(hMemDC);	::DeleteObject(hb);
			Sleep(80);
			dc.Rectangle(xf, (int)(Y - 657 * km-zd), xf + 10, Y);
			xf += 10;
			/*// F_3
			hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_3));
			hMemDC = ::CreateCompatibleDC(NULL); SelectObject(hMemDC, hb);
			::StretchBlt(dc.m_hDC, xf, Y - 674 * km-zd, 316 * km, 674 * km, hMemDC, 0, 0, 316, 674, SRCCOPY);
			::DeleteDC(hMemDC);	::DeleteObject(hb);
			Sleep(20);
			dc.Rectangle(xf, Y - 674 * km-zd, xf + 10, Y);
			xf += 10;*/
		}

		//MessageBox(L"1", L"ZAMOK", MB_OK);
		///////////////////////////Timer<<<<<<<<<<<<<<<<<<<<<<<
		tim = 1;
		SetTimer(3, 1000, NULL);
		while (tim > 0)
		{
			if (PeekMessage(&mes, NULL, 0, 0, PM_REMOVE))
			{
				TranslateMessage(&mes);
				DispatchMessage(&mes);
			}
		}
		KillTimer(3);
		/////////////////////////

		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_F1));
		hMemDC = ::CreateCompatibleDC(NULL); SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, xf-10, (int)(Y - 702 * km-zd), (int)(672 * km), (int)(702 * km), hMemDC, 0, 0, 672, 702, SRCCOPY);
		::DeleteDC(hMemDC);	::DeleteObject(hb);
		///////////////////////////Timer<<<<<<<<<<<<<<<<<<<<<<<
		tim = 3;
		SetTimer(4, 1000, NULL);
		while (tim > 0) {
			if (PeekMessage(&mes, NULL, 0, 0, PM_REMOVE))
			{
				TranslateMessage(&mes);
				DispatchMessage(&mes);
			}
		}
		KillTimer(4);
		/////////////////////////
			
        dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
        mybrush.CreateSolidBrush(RGB(127, 127, 127)); pOldBrush = dc.SelectObject(&mybrush);
        hpen.CreatePen(PS_SOLID, 1, RGB(127, 127, 127));	pOldPen = dc.SelectObject(&hpen);
        dc.Rectangle(0, 0, X, Y); 
		//dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_DR2));
		hMemDC = ::CreateCompatibleDC(NULL); SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, tx, 0, sir, dln, hMemDC, 0, 0, 1220, 1062, SRCCOPY);
		::DeleteDC(hMemDC);	::DeleteObject(hb);
		/*Sleep(50);
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_F1));
		hMemDC = ::CreateCompatibleDC(NULL); SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, (int)(xf - 10-672*km), (int)(Y - 702 * km-zd), (int)(672 * km), (int)(702 * km), hMemDC, 0, 0, 672, 702, SRCCOPY);
		::DeleteDC(hMemDC);	::DeleteObject(hb);
		Sleep(50);*/
		//zakr serim feanora
		//mybrush.CreateSolidBrush(RGB(127, 127, 127)); pOldBrush = dc.SelectObject(&mybrush);
		//hpen.CreatePen(PS_SOLID, 1, RGB(127, 127, 127));	pOldPen = dc.SelectObject(&hpen);
		//dc.Rectangle(xf - 10, (int)(Y - 702 * km-zd), (int)(xf-10+672 * km), Y);
		xf = tx - 282 * km;
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_DR1));
		hMemDC = ::CreateCompatibleDC(NULL); SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, xf, (int)(Y - 653 * km)-zd, (int)(282 * km), (int)(653 * km), hMemDC, 0, 0, 282, 653, SRCCOPY);
		::DeleteDC(hMemDC);	::DeleteObject(hb);
		///////////////////////////Timer<<<<<<<<<<<<<<<<<<<<<<<
		tim = 1;
		SetTimer(5, 1000, NULL);
		while (tim > 0) {
			if (PeekMessage(&mes, NULL, 0, 0, PM_REMOVE))
			{
				TranslateMessage(&mes);
				DispatchMessage(&mes);
			}
		}
		KillTimer(5);
		/////////////////////////
		while (xf + 312 * km > X -1590*koef_zam)
		{// F_2
			hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_DR1));
			hMemDC = ::CreateCompatibleDC(NULL); SelectObject(hMemDC, hb);
			::StretchBlt(dc.m_hDC, xf, (int)(Y - 653 * km)-zd, (int)(282 * km), (int)(653 * km), hMemDC, 0, 0, 282, 653, SRCCOPY);
			::DeleteDC(hMemDC);	::DeleteObject(hb);
			Sleep(80);
			dc.Rectangle(xf+282*km-10, (int)(Y - 653 * km - zd), xf + 282*km, Y);
			xf -= 10;
		}
		
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_DR3));
		hMemDC = ::CreateCompatibleDC(NULL); SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, (int)(X - 1590 * koef_zam), 0, (int)(1590 * koef_zam), (int)(1064 * koef_zam), hMemDC, 0, 0, 1590, 1064, SRCCOPY);
		::DeleteDC(hMemDC);	::DeleteObject(hb);
		///////////////////////////Timer<<<<<<<<<<<<<<<<<<<<<<<
		tim = 1;
		SetTimer(6, 1000, NULL);
		while (tim > 0) {
			if (PeekMessage(&mes, NULL, 0, 0, PM_REMOVE))
			{
				TranslateMessage(&mes);
				DispatchMessage(&mes);
			}
		}
		KillTimer(6);
		/////////////////////////
		while (xf > 0)
		{
			
			hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_DR4));
			hMemDC = ::CreateCompatibleDC(NULL); SelectObject(hMemDC, hb);
			::StretchBlt(dc.m_hDC, xf, (int)(Y - 794 * km)-zd, (int)(498 * km), (int)(794 * km), hMemDC, 0, 0, 498, 794, SRCCOPY);
			::DeleteDC(hMemDC);	::DeleteObject(hb);
			Sleep(80);
			dc.Rectangle(xf + 498 * km - 10, (int)(Y - 794 * km - zd), xf + 498 * km, Y);
			xf -= 10;
		}
		
		///////////////////////////Timer<<<<<<<<<<<<<<<<<<<<<<<
		iffea2 = 1; tim = 3;
		SetTimer(7, 1000, NULL);
		while (tim > 0) {
			if (PeekMessage(&mes, NULL, 0, 0, PM_REMOVE))
			{
				TranslateMessage(&mes);
				DispatchMessage(&mes);
			}
		}
		KillTimer(7);
		/////////////////////////
		dc.Rectangle(0, 0, X, Y);
		dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_DR4));
		hMemDC = ::CreateCompatibleDC(NULL); SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, X/2-498*0.8/2, (int)(Y - 794 * 0.8), (int)(498 * 0.8), (int)(794 * 0.8), hMemDC, 0, 0, 498, 794, SRCCOPY);
		::DeleteDC(hMemDC);	::DeleteObject(hb);
		///////////////////////////Timer<<<<<<<<<<<<<<<<<<<<<<<
		tim = 3;
		SetTimer(8, 1000, NULL);
		while (tim > 0) {
			if (PeekMessage(&mes, NULL, 0, 0, PM_REMOVE))
			{
				TranslateMessage(&mes);
				DispatchMessage(&mes);
			}
		}
		KillTimer(8);
		/////////////////////////

		mybrush.CreateSolidBrush(RGB(0, 0, 0)); pOldBrush = dc.SelectObject(&mybrush);
		hpen.CreatePen(PS_SOLID, 1, RGB(0, 0, 0));	pOldPen = dc.SelectObject(&hpen);
		dc.Rectangle(0, 0, X, Y + 10); 
		dc.SelectObject(pOldPen); hpen.DeleteObject(); dc.SelectObject(pOldBrush); mybrush.DeleteObject();
		hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_K_DR5));
		hMemDC = ::CreateCompatibleDC(NULL); SelectObject(hMemDC, hb);
		::StretchBlt(dc.m_hDC, (int)(X/2-512/2), (int)(Y/2-370/2), 512, 370, hMemDC, 0, 0, 512, 370, SRCCOPY);
		::DeleteDC(hMemDC);	::DeleteObject(hb);
		dc.SetBkMode(TRANSPARENT);
		MyFont.CreateFont(Y / 7, 0, 0, 0, 700, FALSE, FALSE, 0, ANSI_CHARSET,
			OUT_DEFAULT_PRECIS, CLIP_DEFAULT_PRECIS,
			DEFAULT_QUALITY, DEFAULT_PITCH | FF_SWISS,
			L"Complex");
		dc.SelectObject(&MyFont);
		dc.SetTextColor(RGB(168, 0, 0));
		dc.TextOut(X / 2 - (Y / 7) * 3, 10, L"ВЫ ПРОИГРАЛИ...");
		//0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
	}
	pMenu->EnableMenuItem(ID_BASCHNJA, MF_ENABLED);
	pMenu->EnableMenuItem(ID_THOR_L, MF_ENABLED);
	pMenu->EnableMenuItem(ID_THOR_SR, MF_ENABLED);
	pMenu->EnableMenuItem(ID_THOR_SL, MF_ENABLED);
	iffea = 0; iffea2 = 0;
}



void CMFCmyProectDlg::feaprw_ris()
{
	CClientDC dc(this);//один раз на функцию
	
	HBITMAP hb;
	HDC hMemDC;
	int xf = 100;
	
	hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_PRIG));
	hMemDC = ::CreateCompatibleDC(NULL);
	SelectObject(hMemDC, hb);
	::StretchBlt(dc.m_hDC, xf, Y*0.8 - 625 * 0.5-70, 339 * 0.5, 625 * 0.5,//адресат-экран
		hMemDC, 0, 0, 339, 625, SRCCOPY);
	::DeleteDC(hMemDC);
	::DeleteObject(hb);
}
void CMFCmyProectDlg::feaprd_ris()
{
	CClientDC dc(this);//один раз на функцию

	HBITMAP hb;
	HDC hMemDC;
	int xf = 100;

	hb = ::LoadBitmap(::AfxGetInstanceHandle(), MAKEINTRESOURCE(IDB_F_LET));
	hMemDC = ::CreateCompatibleDC(NULL);
	SelectObject(hMemDC, hb);
	::StretchBlt(dc.m_hDC, xf, Y*0.8 - 588 * 0.5 - 70,618 * 0.5, 588* 0.5,//адресат-экран
		hMemDC, 0, 0, 618, 588, SRCCOPY);
	::DeleteDC(hMemDC);
	::DeleteObject(hb);
}

void CMFCmyProectDlg::OnSysKeyDown(UINT nChar, UINT nRepCnt, UINT nFlags)
{
	if (iffea == 1) {
		if (nChar == 39)
		{
			feapd = 1; 
		}
		
	}

	CDialogEx::OnSysKeyDown(nChar, nRepCnt, nFlags);
}
