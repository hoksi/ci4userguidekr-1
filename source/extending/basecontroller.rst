************************
컨트롤러 확장
************************

CodeIgniter의 핵심 컨트롤러는 변경해서는 안되지만 기본 클래스 확장은 **app/Controllers/BaseController.php**\ 에서 제공됩니다.
새로운 컨트롤러는 ``BaseController``\ 를 확장하여 미리 로드된 구성 요소와 제공하는 추가 기능을 활용해야합니다.

::

	<?php 
	
	namespace App\Controllers;
	
	use CodeIgniter\Controller;
	
	class Home extends BaseController {
		// ...
	}

사전로드 구성 요소
=====================

기본 컨트롤러는 프로젝트가 실행될 때마다 사용할 헬퍼, 모델, 라이브러리, 서비스등을 로드하기에 좋은 장소입니다.
사전 정의된 ``$helpers`` 배열에 헬퍼를 추가해야 합니다.
다음 예는 HTML 및 텍스트 헬퍼를 사용할 수 있게 합니다.

::

	protected $helpers = ['html', 'text'];

로드할 다른 구성 요소나 처리할 데이터는 생성자 ``initController()``\ 에 추가해야 합니다.
예를 들어, 프로젝트가 세션 라이브러리를 많이 사용한다면 여기에서 시작할 수 있습니다

::

	public function initController(...)
	{
		// Do Not Edit This Line
		parent::initController($request, $response, $logger);
		
		$this->session = \Config\Services::session();
	}

추가 메소드
==================

베이스(base) 컨트롤러는 라우팅할 수 없습니다.(시스템 구성이 이를 404 페이지 찾을 수 없음으로 라우팅함)
추가된 보안 수단으로, 새로운 생성된 **all** 메소드는 ``protected``\ 나 ``private``\ 으로 선언하고 ``BaseController``\ 를 확장하여 생성한 컨트롤러를 통해서만 액세스합니다.

다른 옵션
=============

하나 이상의 기본 컨트롤러가 필요할 수 있습니다. 
다른 베이스 컨트롤러는 올바른 베이스를 확장하여 새 베이스 컨트롤러를 만들 수 있습니다.
예를 들어, 프로젝트에 공용 인터페이스와 간단한 관리 포털이 있는 경우 ``BaseController``\ 를 공용 컨트롤러로 확장하고 
모든 관리 컨트롤러에 대해 새로 작성된 ``AdminController``\ 를 확장하여 만들 수 있습니다.

베이스 컨트롤러를 사용하지 않으려면 대신 컨트롤러가 시스템 컨트롤러를 확장하도록 하여 베이스 컨트롤러를 무시할 수 있습니다

::

	class Home extends \CodeIgniter\Controller
	{
	
	}
