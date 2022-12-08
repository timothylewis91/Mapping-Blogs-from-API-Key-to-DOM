# Mapping-Cards

 
const [pageData, setPageData] = useState({
    arrayOfBlog: [],
    blogComponents: [],
    pageIndex: 0,
    pageSize: 6,
    totalCount: 0,
    current: 1,
  });
  
   blogService
      .getPage(pageData.pageIndex, pageData.pageSize)
      .then(onGetBlogSuccess)
      .catch(onGetBlogError);
  }, [pageData.pageIndex, pageData.pageSize]);
  
  
const onGetBlogSuccess = (response) => {
    setPageData((prevState) => {
      const bd = { ...prevState };
      bd.arrayOfBlog = response.item.pagedItems;
      bd.totalCount = response.item.totalCount;
      bd.blogComponents = bd.arrayOfBlog.map(mapBlog);
      return bd;
    });
    
    
     <React.Fragment>
      <div className="pt-9 pb-9 bg-white ">
        <Container>
          <Row>
            <Col
              lg={{ span: 10, offset: 1 }}
              xl={{ span: 8, offset: 2 }}
              md={12}
              sm={12}
            >
              <div className="text-center mb-5">
                <h1 className=" display-2 fw-bold">Blogs</h1>
                <p className="lead">
                  Read latest horse news, learn expert horse care tips & improve
                  your riding with tips from pros. Health news, veterinary
                  advice, and educational tools to keep your horse healthy.
                </p>
              </div>

              <Form className="row px-md-20" onSubmit={onBlogSearch}>
                <Form.Group
                  className="mb-3 col ps-0 ms-2 ms-md-0"
                  controlId="formBasicEmail"
                >
                  <Form.Control
                    type="search"
                    placeholder="Search"
                    onChange={onSearchBlogChange}
                  />
                </Form.Group>
                <Form.Group
                  className="mb-3 col-auto ps-0"
                  controlId="formSubmitButton"
                >
                  <Button variant="primary" type="submit">
                    Search
                  </Button>
                </Form.Group>
              </Form>

              <select
                className=" blogDropdown-category form-group"
                onChange={onBlogCatergory}
              >
                <option value={""}>Please select</option>
                {blogCatergory?.mappedBlogCat}
              </select>
            </Col>
          </Row>
        </Container>
      </div>
      <div className="pb-8 bg-white">
        <Container>
          {restrictedToAdmin()}
          <Row>{pageData.blogComponents}</Row>
        </Container>
        <Pagination
          className="blog-card-pagination mx-auto"
          onChange={onBlogChange}
          current={pageData.pageIndex + 1}
          total={pageData.totalCount}
          pageSize={pageData.pageSize}
          locale={locale}
        />
      </div>
    </React.Fragment>
    
    
    
    <Col className="d-flex col-xl-4 col-lg-4 col-md-6 col-sm-12">
      <Card className="blog-cards mb-4 shadow-lg shadow-lg p-3 mb-5 bg-body rounded">
        <a>
          {" "}
          <Image
            src={props.item.imageUrl}
            alt="blogProfile"
            className="blogs-square-pictures card-img-top rounded-top-md img-fluid"
          />
        </a>
        <Card.Body>
          <h3>
            <p className="blog-subject ">{props.item.title}</p>
          </h3>
          <p className="text-blog-content-input">{props.item.subject}</p>
          <Row className="align-items-center g-0 mt-4">
            <Col className="col-auto col">
              <Col className="align-items-center g-0 mt-4 row">
                <div className="col-auto col">
                  <p className="fs-6 mb-0"> </p>
                </div>
                <div className="col-12 container">
                  <div className=" row">
                    <div className=" col">
                      {restrictedRoles()}
                      <Button
                        type="button"
                        className="btn btn-success"
                        onClick={onNavViewClicked}
                      >
                        View
                      </Button>
                    </div>
                  </div>
                </div>
              </Col>
            </Col>
          </Row>
          <Col>
            <div className="p-5 d-flex col-auto col">
              <Image
                src={horseHeart}
                alt="blogProfile"
                className="rounded-circle avatar-sm me-2"
              />{" "}
              <div className="card-blogging-text-col 1h-1 col">
                <p className="fs-6 mb-0">{datePublished}</p>
              </div>
            </div>
          </Col>
        </Card.Body>
      </Card>
    </Col>
