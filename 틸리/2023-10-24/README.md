<h3>1. router.isReady 메서드 사용하기</h3><p><code>router.isReady</code>는 라우터 필드가 클라이언트 측에서 업데이트되고 사용할 준비가 되었는지 여부를 확인하는 메서드이다.</p><p>이 방법은 Next.Js@10.0.5이후에 추가된 기능이라고 한다.</p><pre><code class="language-plaintext">  useEffect(() =&gt; {
      if (!router.isReady) return;
      router.query.pvId &amp;&amp;
        setSkuInfo({ ...skuInfo, productVariationId: Number(router.query.pvId) });
    }, [router.isReady]);</code></pre><p>위와 같은 useEffect를 추가해두면, router가 준비되었을 때에 다시 skuInfo를 업데이트 해주어서, input창에 원하는 값을 넣을 수 있다.</p><p>&nbsp;</p><h3>2. getServerSideProps 이용하기</h3><p>serverSideProps에서 context로 전달된 query를 컴포넌트에 넘겨주어 사용하기</p><p>context 안에는 아래와 같은 정보들이 담겨있다.</p><pre><code class="language-plaintext">type Context = {
    req: IncomingMessage; // http 요청
    res: ServerResponse; // http 응답
    pathname: string; // url 경로
    query: ParsedUrlQuery; // 쿼리문자열
    asPath: string; // 쿼리 문자열 포함한 요청 경로
    AppTree: React.ComponentType; // next js 루트 구성요소
  };</code></pre><p>이 중에서 query 정보를 props로 넘겨주면, isReady 메서드 없이 상위 상품의 id를 바로 불러올 수 있다</p><pre><code class="language-plaintext">const SkuCreatePage = ({ pvId }: P) =&gt; {
    return &lt;CreateSku pvId={pvId} /&gt;;
  };
  
  export default SkuCreatePage;
  
  export const getServerSideProps = async (context: NextPageContext) =&gt; {
    const { query } = context;
    const { pvId } = query;
    return { props: { pvId } };
  };</code></pre><p>&nbsp;</p><p>컴포넌트가 렌더링 될 때에 router.query를 바로 받아올 수 있는 방법을 2가지나 알게되었으니,,</p><p>이제 쿼리를 사용하여 여러가지 데이터를 넘기고 사용하는 방법을 좀더 활용해서 기능을 구현해보도록 해야겠다~~</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p>